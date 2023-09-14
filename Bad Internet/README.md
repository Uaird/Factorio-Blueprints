![image](https://github.com/Uaird/Factorio-Blueprints/assets/96286260/50300699-2095-479d-a1ed-ac44f80fdf2d)

Included in the book is a blueprint called "Original Design". It uses Nixie Tubes, Text Plates, and Pushbuttons. All other blueprints are vanilla.

 
 
 	\\C_DETECT means collision detection, if it's >1, it means two or more items are trying to do something on the line.
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



	FAST REQUEST NODE:
	
		INPUT 		1	-	-	-	-	-	-	-
		READ 		-	-	-	-	-	1	-	-
		READ_RST	-	-	-	-	-	-	-	1
		WRITE		-	-	-	-	-	1	-	-
		WRITE_RST	-	-	-	-	-	-	-	1
		
		TICK		1	2	3	4	5	6	7	8
	
	
	
	MEMORY NODE:
	
		SIGNAL		1	-	-	-	-	-	-	-
		READ		-	-	1	-	-	-	-	-
		WRITE_CLR	-	-	-	1	-	-	-	-
		WRITE_RCVD	-	-	-	1	-	-	-	-
		WRITE		-	-	-	-	1	-	-	-
		
		TICK		1	2	3	4	5	6	7	8
