<pre>
School of Information Technologies and Engineering, ADA University
CSCI3510 – Principles of Operating Systems 
Spring 2025 – 3/7/2025
Assignment 1 by Laman Panakhova 16882
</pre>

<pre>
**Readers-Writers Problem with Load Balancing**
</pre>

<pre>
**Instructions**
</pre>


This project implements a solution to the Readers-Writers problem with load balancing. 
The program ensures writer priority over readers and balances the load of readers across multiple file replicas. 
The solution uses threads, synchronization mechanisms (mutexes, condition variables, and semaphores), and logs every read/write operation.

Multiple reader threads operate at random time intervals and read from one of the file replicas.
A single writer thread on a timely bases writes to all file replicas.

**The system focuses mainly on:**
1. That writers are given priority over readers.
2. That readers are distributed across file replicas evenly.
3. The writer locks all file replicas simultaneously and updates their contents.

**Features implemented in the code**
1. Fairness: Writers are given priority, and readers must wait for writers to finish their work.
2. Load Balancing: Readers are distributed evenly across all file replicas.
3. Thread Safety: The program ensures that no two threads access the same file meanwhile.
4. Logging: Logs every read and write operation by including file access details and content.
5. Randomization: Reader threads start at random time intervals, and the writer thread sleeps randomly between write operations.

<pre>
Requirements:
</pre>
Programming Language: C

<pre>
Libraries used in the code:
</pre>
1. pthread.h (for threading)
2. semaphore.h (for semaphore management)
3. stdio.h (for logging)
4. stdlib.h (for random number generation)
5. unistd.h (for sleep functions)
6. fcntl.h (for file handling)
7. string.h (for string manipulation)
8. time.h (for random seed generation)

<pre>
Compilation and Running the Program
</pre>

Prerequisites:
Ensure that you have a C compiler installed (e.g., GCC). 
The program also uses POSIX threads and semaphores, so your system should support these libraries.

You can clone this rep by these steps:
-bash
-Copy
-Edit
-git clone <repository_url>
-cd <repository_directory>

To compile the program, run the following command in your terminal:
-bash
-Copy
-Edit
-gcc -o readers_writers readers_writers.c -lpthread

After compiling, you can run the program using the following command:
-bash
-Copy
-Edit
./readers_writers

The program will create a log.txt file that logs all the operations performed by the reader and writer threads. 
You can inspect this log to see the system's behavior.

<pre>
Program Flow
</pre>

**Reader Threads:**
A set number of reader threads are created.
Each reader thread attempts to read from one of the file replicas, based on load balancing.
If a writer is active, readers will wait until the writer finishes.

**Writer Thread:**
The writer thread from time to time attempts to write to all three file replicas.
It locks all replicas simultaneously to ensure consistent content across all files.
While the writer is active, no readers are allowed to access the files.

**Logging in the code:**
At this step every read and write operation is logged, including the file being accessed, the number of readers, the active status of the writer, and the file content.

**Termination of the program:**
The program will run until that moment when all reader threads finish and the writer thread completes its operations.

**Example Output**
In the terminal, you will see the output similar to the following for reader and writer threads:

Main here. Creating writer thread
Main here. Creating reader thread 0
Reader 0 reading from file1.txt
Main here. Creating reader thread 1
Reader 1 reading from file2.txt
Writer modifying all replicas...
The log file (log.txt) will contain information such as:

Writer active: 1
Readers on file1.txt: 1
Readers on file2.txt: 1
Readers on file3.txt: 0
Content of file1.txt: Updated content by writer
Content of file2.txt: Updated content by writer
Content of file3.txt: Updated content by writer

**Code Structure**
readers_writers.c: The main program file containing the implementation.
log.txt: The log file created by the program to track operations.
Makefile (if applicable): For building the project (if you decide to use one).
Design and Synchronization Mechanism in the program 

**Our program uses a combination of:**
**Mutexes:** Was used for mutual exclusion when changing shared resources like the file replicas and the readers_count array.
**Condition Variables:** Was used to synchronize reader and writer threads when the writer is active.
**Semaphores:** Was used to ensure the writer thread that it operates without conflicts.

**If you want a more detailed explanation of the design, please refer to the assignment report.**
<pre>
Some Drawbacks & Potential Improvements:
</pre>
Our program currently uses random sleep times for the purposes of simulation, which may not cover all edge cases.
The current implementation logs file content directly, which might not be efficient for very large files.
Optimizing log handling to avoid repeatedly opening/closing files.
Implementing a more advanced load balancing algorithm for readers.
Graceful thread termination and resource cleanup after execution.

lpanakhova16882@ada.edu.az
For questions or feedback, feel free to reach out.
