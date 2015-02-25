# sards
Statistical Analaysis of Random Data Sets
=========================================

This project was developed to quickly compare variously generated sets of random data as to their relative quality of randomness to one another. It is based on the NIST sts-2.1.2 battery of statistical evaluations.  Data is passed in via a pipe and is broken into 10 streams( or batches) of 100000 bits each.  Each stream is then passed through the battery of tests.  As the test runs an overall passing rate of batches is calculated.  Ouput is produced when a test batch does not achieve a ratio of passes > 7 out of 10 for a given test. When this failure is detected a line is produced to the screen displaying A) the overall pass rate of all test batches, B) the ratio of passes to batch size for the failing test and C) the name of the test that failed for the batch. 

NOTE:  All tests from the battery are executed over the incoming data stream, however, the results from Universal test and the NonOverlapping test are currently being discarded for a couple of reasons.  The Universal test is failing for every data stream passed into the unmodified sts-2.1.2 suite and consequently our modification.  The NonOverlapping test produces multiple evaluations over the same batch of streams and therefore skews our results.

DISCLAIMER!   The original suite was menu driven and not conducive to quick and flexible execution. This work is, to put it mildly a hack job of an apparent hack job, based on the sts-2.1.2 test suite from NIST.  Precedence was given to speed of development not to quality of code.  

The original sts-2.1.2 suite is available from NIST [here](http://csrc.nist.gov/groups/ST/toolkit/rng/documentation_software.html). 
The documentation for the analyses performed and the code can be found [here](http://csrc.nist.gov/publications/nistpubs/800-22-rev1a/SP800-22rev1a.pdf).




Install and Use
---------------
Use git to checkout the current copy of this suite
From the project directory create the directories that will hold working files during execution and the final test results.

$testhost ~/sards$ experiments/create-dir-script

Modify the makefile as necessary and compile the code

Run the the assess executable passing in a stream of binary data.
$testhost ~/sards$ cat /dev/urandom | ./assess

Output produced for a non-random data set, such as for and .mp4 here, will be similar to following:
0.0%     4/10   *  Frequency
0.0%     4/10   *  BlockFrequency
0.0%     4/10   *  CumulativeSums
0.0%     5/10   *  LongestRun
0.0%     6/10   *  Rank
0.0%     7/10   *  FFT
10.0%     2/10   *  ApproximateEntropy
9.1%     3/10   *  Serial
14.3%     5/10   *  Frequency
13.3%     5/10   *  BlockFrequency
12.5%     2/10   *  CumulativeSums
11.1%     2/10   *  Runs
10.5%     5/10   *  LongestRun
21.7%     1/10   *  ApproximateEntropy
20.8%     3/10   *  Serial


and the following for a random data set such as /dev/urandom
90.0%     6/10   *  ApproximateEntropy
91.3%     6/10   *  ApproximateEntropy
93.9%     7/10   *  ApproximateEntropy
93.5%     7/10   *  ApproximateEntropy
95.6%     7/10   *  ApproximateEntropy
95.7%     7/10   *  ApproximateEntropy
95.4%     6/10   *  ApproximateEntropy
95.2%     6/10   *  ApproximateEntropy
95.0%     6/10   *  ApproximateEntropy
94.8%     6/10   *  ApproximateEntropy
94.6%     6/10   *  ApproximateEntropy
94.5%     7/10   *  ApproximateEntropy

