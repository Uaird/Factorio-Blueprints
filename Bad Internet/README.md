# Bad Internet

Ever need to use more than one wire, but don't want to? This project enables you to read and write information from nodes connected to a single wire. The instructions are in the blueprint.

![image](https://github.com/Uaird/Factorio-Blueprints/assets/96286260/c63372cc-8474-41a5-806a-c528ce1d9cab)



Included in the book is a blueprint called "Original Design". It uses Nixie Tubes, Text Plates, and Pushbuttons. All other blueprints are vanilla.
The R%15 combinator in the client node blueprint sets the average amount of ticks to retry in the event of a collision. You can change the number to higher values for particularly large networks.


# Example Usage

A read-only node has been connected to a client node. We're going to try to read what's in the chest.

![image](https://github.com/Uaird/Factorio-Blueprints/assets/96286260/ba806033-be0c-4200-8e07-eed4f9676f71)


1. Change the address of the read-only node. I'll just set it to address 123 by setting white to -123.

<img src="https://github.com/Uaird/Factorio-Blueprints/assets/96286260/c0e06580-5706-4244-b94f-cf8ee9660e20" width="600" height="450">

2. We'll need to save the output pulse and display it, so we'll use a simple SR latch and nixie tubes.
   
<img src="https://github.com/Uaird/Factorio-Blueprints/assets/96286260/e93c25b4-8df5-4987-8dc5-08b39ec7131a" width="600" height="450">

3. Now all we have to do is apply the read signal. Black=1 for collision detection, gray=1 for read, and white=123 for the address. Then flip the switch on.

 <img src="https://github.com/Uaird/Factorio-Blueprints/assets/96286260/d264fee1-233d-4a7c-99f2-88bb88d34d62" width="600" height="450">

 4. ...and voila! It's output the value.

 <img src="https://github.com/Uaird/Factorio-Blueprints/assets/96286260/c5a6d8fe-77e1-4e33-8242-d44343eefea92" width="600" height="450">

 #Technical Notes



 
 
 	\\C_DETECT means collision detection, if it's >1, it means two or more nodes are trying to do something on the line.
	\\WRITE_RCVD is a confirmation that the input signal has been written
	\\No plans for congestion handling

	\\C_DETECT	BLACK	=1
	\\READ OUT	GRAY	=0
	\\READ		GRAY	=1
	\\WRITE		GRAY	=2
	\\WRITE_RCVD	GRAY	=3
	\\ADDRESS	WHITE	=$ADDRESS



			BLACK		WHITE		GRAY	ETC

	READ REQUEST:
	
 		IN:	C_DETECT	ADDRESS		READ	-
		OUT:	C_DETECT	ADDRESS		-	INFO

	WRITE REQUEST:
	
		IN:	C_DETECT	ADDRESS		WRITE	INFO
		OUT:	C_DETECT	ADDRESS		RCVD	-



	FAST CLIENT NODE:
	
		INPUT 		1	-	-	-	-	-	-	-
		READ 		-	-	-	-	-	1	-	-
		READ_RST	-	-	-	-	-	-	-	1
		WRITE		-	-	-	-	-	1	-	-
		WRITE_RST	-	-	-	-	-	-	-	1
		
		TICK		1	2	3	4	5	6	7	8
	
	
	
	RW MEMORY NODE:
	
		SIGNAL		1	-	-	-	-	-	-	-
		READ		-	-	1	-	-	-	-	-
		WRITE_CLR	-	-	-	1	-	-	-	-
		WRITE_RCVD	-	-	-	1	-	-	-	-
		WRITE		-	-	-	-	1	-	-	-
		
		TICK		1	2	3	4	5	6	7	8


![image](https://github.com/Uaird/Factorio-Blueprints/assets/96286260/e0175434-5393-41fe-a3f6-a329c9e34991)
