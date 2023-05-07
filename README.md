Download Link: https://assignmentchef.com/product/solved-operatingsystems-problem-2-multi-threaded-coin-flipping
<br>
<strong>Problem 2.1: </strong><em>multi-threaded coin flipping</em>

There are 20 coins lying in a row on a table. <em>P </em>persons flip all 20 coins lying on the table <em>N </em>times. Write a program that emulates this by using threads, one thread emulating one person. By default, there are <em>P </em>=100 persons and each person flips all 20 coins <em>N </em>=10000 times. Implement command line options to control the number of persons (-p) and the number of times a person flips all coins on the table (-n).

Use a global array of characters to represent the coins, where an X represents one side of a coin and a 0 represents the other side of a coin. Print the coins on the standard output before the coin flipping starts and print the coins when all persons have finished flipping coins. In addition, print the time it took for all persons to flip the coins.

You must ensure that no coin is flipped by another person, while one person has his turn. Implement three strategies:

<ol>

 <li>In the first strategy, you use a global lock to protect the coins. A person first obtains the global lock covering all coins and then the person flips <em>N </em>times all 20 coins and finally, when done flipping coins, the person releases the lock.</li>

 <li>In the second strategy, you also use a global lock but a person obtains the lock for each iteration, i.e., a person obtains the lock, flips the 20 coins, releases the lock, and then moves to the next iteration.</li>

 <li>In the third strategy, there is a lock for each coin, i.e., a person obtains a lock for a coin, flips the coin, and releases the lock immediately after each coin flip.</li>

</ol>

Let your program measure the time it took all persons to flip all coins and write the results to the standard output. An example execution might look as follows (actual times replaced by underscores):

$ ./coins coins: 0000000000XXXXXXXXXX (start – global lock) coins: 0000000000XXXXXXXXXX (end – global lock) 100 threads x 10000 flips:  ____.___ ms

coins: 0000000000XXXXXXXXXX (start – iteration lock) coins: 0000000000XXXXXXXXXX (end – table lock) 100 threads x 10000 flips:              ____.___ ms

coins: 0000000000XXXXXXXXXX (start – coin lock) coins: 0000000000XXXXXXXXXX (end – coin lock) 100 threads x 10000 flips:             ____.___ ms

Submit the times you measured. What do you observe?

Time measurement can be done in a simple (although not very accurate) manner. The timeit() function shown below takes as arguments the number of threads and a pointer to a function implementing one of the three coin flipping strategies. The run_threads() function creates n threads (each one executing proc) and joins them again. The calls to clock() obtain the a timestamp before and a timestamp after the execution of run_threads(). The timestamps are then used calculate the execution time (in microseconds).

static double timeit(int n, void* (*proc)(void *))

{ clock_t t1, t2; t1 = clock(); run_threads(n, proc); t2 = clock(); return ((double) t2 – (double) t1) / CLOCKS_PER_SEC * 1000;

}