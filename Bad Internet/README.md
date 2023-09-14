# Bad Internet

Ever need to use more than one wire, but don't want to? This project enables you to read and write information from nodes connected to a single wire. The instructions are in the blueprint.

![image](https://github.com/Uaird/Factorio-Blueprints/assets/96286260/c63372cc-8474-41a5-806a-c528ce1d9cab)



Included in the book is a blueprint called "Original Design". It uses Nixie Tubes, Text Plates, and Pushbuttons. All other blueprints are vanilla.
The R%15 combinator in the request node blueprint sets the average amount of ticks to retry in the event of a collision. You can change the number to higher values for particularly large networks.

 
 
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
