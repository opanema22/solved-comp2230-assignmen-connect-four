Download Link: https://assignmentchef.com/product/solved-comp2230-assignmen-connect-four
<br>
<h1></h1>

Connect four is a two player game. The objective of the game is to connect four markers in sequence, in either a row, column or diagonal, while preventing your opponent from doing the same. The game is won when a player makes four markers in a sequence.

The game is played by placing a marker in one of seven columns, and the marker is placed on the lowest row in that column. There are six rows in each column to make a play field of 7 × 6. Players take turns placing markers.

<h1>Requirements</h1>

<ul>

 <li>Language: Java 1.8</li>

 <li>The engine must use minimax, or some derivation of minimax, such as the refactored negamax or the faster, but more complex alpha-beta pruning heuristic.</li>

 <li>The evaluation function associated with the engine can be as complicated or as simple as you like, as long as it correctly identifies a win, loss, or draw with appropriate values. Appropriate values might be for example a large positive number for the first player winning, a large negative number for the second player winning, and 0 for a draw, although this specific heuristic is not required, other heuristics can work.</li>

 <li>The engine must parse the input correctly to set up the game state internally. It must also pass out the output in the correct format.</li>

 <li>There is no fixed requirement on how to store the game state, whichever you deem to be the best for your individual engine is acceptable.</li>

 <li>All communication will be done over standard input and output.</li>

 <li>The engine must correctly behave under all possible coordinator commands.</li>

</ul>

<h1>Coordinator Commands</h1>

The following are the commands required to interface with the connect four coordinator. All commands will be sent to the engine via System.in in java, and all responses sent from the engine to the coordinator should be done via System.out.println or System.out.print. Note that a new line character needs to be at the end of each command, so using the first option is probably easiest. Each command is case sensitive.

<h2>Sent From the Coordinator</h2>

<ul>

 <li>name – request for the engines name. The reply should be the name of the engine. The name should be whatever name you want to give it, followed by your student number, that is, enginename-cXXXXXXX.</li>

 <li>isready – A command used to synchronise the engine with the coordinator. The reply should be readyok.</li>

 <li>position startpos &lt;moves&gt; – The current order of moves played from the start position. For example, position startpos 0123456. Only the numbers 0−6 will ever be used. This command will always be followed by the isready The only operation allowed to be performed by the engine between receiving this command is to update the internal board with the moves, no searching is allowed.</li>

 <li>go ftime x stime y – Tells the engine to start calculating. The x string will be the time remaining for the first player in milliseconds. The y string will be how long the second player has left. The reply should be bestmove z v where z is the column number, 0 − 6, that the engine wants to place its next marker in. If it is invalid it will be an automatic forfeit. v is the value of the evaluation function after that move. All searching is done here.</li>

 <li>perft x – Tells the engine to count how many nodes are in the entire search tree when expanded to depth x from the current position. The reply should be perft x y where x is the same value passed in, and y is the number of nodes in the search tree when it is expanded to depth x. This should be a separate algorithm to your minimax algorithm, mostly used for debugging and performance testing (hence the name) purposes and be ready to take in any depth.</li>

 <li>quit – Tells the engine to quit. Reply should be quitting.</li>

</ul>

<h2>Sent From Your Engine</h2>

<ul>

 <li>readyok – The response to any isready command only when the engine is ready.</li>

 <li>bestmove z v – The response to the go z is the column the engine wants the next marker in, labeled 0 − 6. v is the value of the evaluation function after that move.</li>

 <li>info – If used, must be after a go command from the coordinator, and before the bestmove response from the engine. It can be followed by a number of optional strings. Each string must be paired with the corresponding data. Not a requirement to use info, it is mainly used for debugging purposes.

  <ul>

   <li>depth x – The depth searched by the engine so far.</li>

   <li>nodes x – The number of nodes searched by the engine so far.</li>

   <li>score x – The current best evaluation by the engine so far.</li>

   <li>string x – Any string the engine wishes to display. If there is a string command, the rest of the line will be interpreted as the string corresponding to the string command.</li>

  </ul></li>

 <li>quitting – The response to the command quit. The engine should exit at this point.</li>

</ul>

<h1>Coordinator.jar</h1>

A file called connect_4_coordinator.jar has been supplied. It is created against java 1.8. It will be used to verify your engine is working correctly and implements everything mentioned in the coordinator commands section. To use the file refer to your IDE’s documentation to see how to run a jar file in it, and adjust the command line arguments for it. If you wish to use it on the command line to run it, I would advise using an ANSI complaint terminal, although this is not necessary.

To run the file from the command line you need to use java -jar connect_4_coordinator.jar along with the arguments to pass to the program. The arguments are:

<ul>

 <li>(required) e0 &lt;path&gt; where &lt;path&gt; is the directory containing the file called Interface which includes the main method of your engine.</li>

 <li>(optional) e1 &lt;path&gt; where &lt;path&gt; is the directory containing a file called Interface which includes the main method of another engine. If this is not used the first engine will be used again, so it is easy to set up a self game for the engine.</li>

 <li>(optional) time x where x is the amount of time in milliseconds each engine is allowed to use. If this is not used, x will be 120000 (2 minutes).</li>

 <li>(optional) perft x where x is the depth the engine should calculate the perft function to.</li>

</ul>

<h1>Sample Communication</h1>

The following is the communication of the setup and first two moves of a game of the same engine playing against itself.

The following is the setup of an engine, along with the perft test of an engine.