# SE4367_MP1

# Part 0: Getting Started
How to execute:
1. Download HelloThread.java and and TestSoot.java
2. Keep both java files in the same "src" package
3. Compile and run TestSoot.java

Modifications to file(s):
1. Change *String mainclass = "HelloThread";* to *String mainclass = "src.HelloThread";* in TestSoot.java

# Part 1: Control Flow Analysis - Finding Denominators
How to execute:
1. Download TestDominatorFInder.java, GCD.java, and DominatorFinder.java
2. Keep all three java files in the same "src" package
3. Compile and run TestDominatorFinder.java

Modifications to file(s):
1. Change *String mainclass = "GCD";* to *String mainclass = "src.GCD";* in TestDominatorFInder.java

Your task: given a method m and a statement s, to find all the statements in m that dominate s.

# Part 2: Data Flow Analysis - Call Graph Construction
How to execute:
1. Download TestSootCallGraph.java and Example.java 
2. Keep both java files in the same default package
3. Compile and run TestSootCallGraph.java

Modifications to file(s):
1. When finding CHA, uncomment enableCHACallGraph(); and comment enableSparkCallGraph(); in TestSootCallGraph.java
2. When finding PTA, uncomment enableSparkCallGraph(); and comment enableCHACallGraph(); in TestSootCallGraph.java
3. Implement a timer to calculate speed with the following code segment in TestSootCallGraph.java:
      //start timer 
	    long startTimer = System.currentTimeMillis();
	    
	    //enable call graph
	    enableCHACallGraph();	// CHA
	    //enableSparkCallGraph();	// PTA 
	    
	    //end timer
	    long endTimer = System.currentTimeMillis();
	    
	    //print out the total runtime
	    System.out.println("Time: " + (endTimer-startTimer));

Answers:
CHA Speed = 255ms
CHA Total Edges = 12
PTA Speed = 1ms
PTA Total Edges = 7
PTA is faster and more accurate than CHA.

# Part 3: Program Instrumentation with Soot
## Logging Method Calls
How to execute:
1. Download TestSootLogging.java and Example.java
2. Keep both java files in the same default package
3. Compile and run TestSootLogging.java
4. Compile and run Example.java

Modifications to file(s):

## Tracing Heap Access
How to execute:
1. Download TestSootLoggingHeap.java and Example.java
2. Keep both java files in the same default package
3. Compile and run TestSootLoggingHeap.java

Modifications to file(s):
1. Change *String mainclass = "HelloThread";* to *String mainclass = "src.HelloThread";*
2. Added the following code segment:
	//your code starts here
		   	    Log log = new Log();
		            boolean isWrite = true;
		            boolean isStatic = ((SootField)stmt.getFieldRef().getField()).isStatic(); 
		    		Class clss = stmt.getDefBoxes().get(0).getValue().getClass();        

		            try {
		             if( (clss == Class.forName("soot.jimple.internal.JInstanceFieldRef")) || (clss == Class.forName("soot.jimple.StaticFieldRef"))  ) {
		              isWrite = true;
		             } 
		             else { isWrite = false; }
		            } catch (Exception e) {}
		            
		            log.logFieldAcc(stmt, stmt.getFieldRef().toString(), isStatic, isWrite);

