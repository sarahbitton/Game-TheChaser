# Game-TheChaser
Information:
Operating systems:
Unix (max OS)
Windows

Programming language:
Python 3.8


Theoretical background:
Definition:
A socket is one endpoint of a two-way communication link between two programs running on the network. A socket is bound to a port number so that the TCP layer can identify the application that data is destined to be sent to.

Generally, the server runs on a specific computer and has a socket that is bound to a specific port number. The server just waits, listening to the socket for a client to make a connection request.
The client knows the hostname of the machine on which the server is running and the port number on which the server is listening. To make a connection request, the client tries to meet with the server on the server's machine and port. The client also needs to identify itself to the server so it binds to a local port number that it will use during this connection. If everything goes well, the server accepts the connection. Upon acceptance, the server gets a new socket bound to the same local port and also get the address and port of the client. On the client side, if the connection is accepted, a socket is successfully created and the client can use the socket to communicate with the server. The client and server can now communicate by writing to or reading from their sockets.
	With the help of sockets, we realized an online version of the game ‘The Chase’. In this game, the player has to answer three questions in order to make his wallet and then, he has to play against the chaser – here an IA – in order to win the wallet he did make for himself.







The code:
Server.py: this file is the main file , we wrote the code step by step to create the game. We accepted the connection with the client and in the end of this file we close the connection.
-	Ask_question: this function receive 3 parameters: the level of the game (1 for the 3 questions of the beginning and 2 when we start playing with the chaser) , qnum is an integer from 0 to 9 , and “with_joker” is a variable we define to know if we used the joker or not. This function called the function get_question and send the question with the answer’s possibilities to the client 
-	Check-answer : the goal of this function is to check the answer of the client : with the precedent function we send the question and in this function we receive the answer of the client. We separate this function in 2 part , the first one is if the client send “joker” then we removed 2 false possibilities of answer and send back the question with just 2 possibilites of answer( we create a new array with just 2 possibilities of answer) the first answer is the correct one then if the client send “A” we know he was right and we increment his step in the game and this wallet. The second part is if the client send of the letter a b c or d , we knew that the correct answer was the last one of the array so we compare the client’answer with the correct one and according to this we change the step and the wallet.
-	On_new_client : this function create a new player: we create a class player and in this function we called the constructor of this class. The object player we create is the client. In this function we create the game step by step: at the beginning we send 3 different questions to the client ( then with the function above we check the answer and update the wallet) , then we send him the choice with the 3 possibilities and with the player’ function we update this step and his wallet. Like the player , we create a class Chaser and in this step of the game we create a chaser with the constructor of this class. Now the player and the chaser are playing: we send to them question , we check their answer and with their respective function we update their step and their wallet while one of then win.
Client.py: this file allows the client to play to the game: at the beginning we establish the connection with the serveur , we send him a message to know if he wants to play to the game and only if he said yes we start to send the questions. 
For the first part the client receive the question with 4 possibilities of response , with the function input we took his answer and send it to the serveur who check by the function check answer if the answer is right or wrong , the serveur send to the client if he ws right or not. After the 3 questions of the beginning the serveur send to the client the question with the “choice” , the client answer and send back to the serveur his choice. 
For the second part , we add the possibilities of “joker”. We define the variable chaser_response as “” at the beginning because we wanted to enter in the first loop which we know correspond to the fact that no one win, like the first part we first check that the answer was one of the acceptable answer and send it to the serveur. While we don’t have winner the serveur continue to send questions. When we have the winner the serveur send it to the client and the client close his connection. 
	

Player.py:
	This file is the class Player. Each time a client connects and wants to play, a new instance of the object Player is created.
-	All the functions get/set/clear are here to return/change a value that qualify the player.
-	change_wallet_step: this function change the wallet of the player in function of his choice in the second part with the chaser. 

Questions.py:
	This file contains all the question in form of a double array, separated in two part for the two part game (one without the chaser with easier questions, one with the chaser with more difficult questions).
	The questions are in form of a list with the first element as the question, the second, third, fourth and fifth as potential answers, and the last as the good answer.
-	get_question: return a question
-	get_answer: return the good answer

SmartChaser.py:
	This file is the class of the SmartChaser. It is used at the second part in order to create the chaser who will be against the player.
-	chose_answer: this function will make the chaser chose an answer when given a list of answers, with a probability of 0.75 to pick the right answer. If it is the good answer, it returns true. If not, false.
-	chaser_answer: this function will take a question and return if the chaser was right or not.



The sockets :
	In the server and client file, we created a socket for each in order for them to communicate.
A socket is one endpoint (combination of an IP address and a port number) of a two-way communication link between two programs running on the network. A socket is bound to a port number so that the TCP layer can identify the application that data is destined to be sent to.  Every TCP connection can be uniquely identified by its two endpoints. That way you can have multiple connections between your host and the server. The Transmission Control Protocol (TCP) is a transport protocol that is used on top of IP to ensure reliable transmission of packets.
Every time a client is connected to the server, the server create a new thread in order to separately communicate with each of the client, so in our game we have 3 different threads : that’s called Multithreading which is a process of executing multiple threads simultaneously in a single process.



 















































































































































































