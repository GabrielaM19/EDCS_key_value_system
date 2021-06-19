# EDCS_key_value_system

The implementation has following features and functions:
The search time efficiency is O(log(N)) by maintaining an 32-entry finger table in each node.

It supports concurrent nodes joining and leaving. This is achieved by implementing the Stabilization part in the Chord paper. The system will always converge to correct status even if it "needs to deal with nodes joining the system concurrently and with nodes that fail or leave voluntarily". Every node will keep communicating with its successor and correcting its finger table. This is implemented by multi-threading programming.

Consistent SHA-1 hashing is used to give identifier to string and socket address.

System allow to add the value, delete the value and update the value inserted previously to the system.


# Implementation of the classes :
The Chord class is responsible for creating the servers and to listen to the clients requests.
The Query class is responsible for client GUI where she or he can add, delete, search, update or quit the system.
The Talker class is responsible for proccessing specific requests from the client and compute them to the form in which client will understand the response from server class.
The Listener class starts the server and keeps it running and listening for the requests.
The Node class created the Node in the whole systems (which plays the role of the server). Initiates the successor, predecessor etc. Also it has the list for keeping the key-values.
The Helper class does the hashing algorithms specific for the Chord protocol.


**Run**
Run Chord

Create a chord ring

  java Chord 8001
Note here the C for Chord is uppercase, and 8050 is the port that you want this node to listen to.

Hopefully you are going to see something like this:

  Joining the Chord ring.
  Local IP: 192.168.65.1

  You are listening on port 8001.
  Your position is 8459f9fa (51%).
  Your predecessor is yourself.
  Your successor is yourself.
Join an existing ring

  java Chord 8010 192.168.65.2 8002
This means you are creating a node that listen to port 8051 and it is joining a ring containing 192.168.65.2:8002.

If the input is right and the port 8010 is not occupied, you will see the following lines:

  Joining the Chord ring.
  Local IP: 192.168.65.2

  You are listening on port 8002.
  Your position is 1ac96434 (10%).
  Your predecessor is updating.
  Your successor is node /192.168.65.1, port 8001, position 8459f9fa (51%).
After you create a node, you could input info at any time to check this node's socket address, predecessor and finger table. You could also terminate this node and leave chord ring by inputing quit or just press ctrl+C.

Run Query

java Query 192.168.65.2
If the program cannot connect to the node you are trying to contact, it will exit. Or if the connection is successful, you will see the following lines:
Please enter one of the options available :
						1. S - search the key
						2. A - add the key
						3. U - update the key
						4. D - delete the key
				    5. quit - exit the system
