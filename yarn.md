# YARN & MapReduce 1
## *Emile .E. EKANE*
## *21/10/2021*
## 

<br><br>

# 1. YARN
In this tutorial, we will use MapReduce examples to learn how to work with Apache YARN
<br><br>

## 1.1 The MapReduce examples
The samples are located on the Hortonworks Data Platform cluster at:
- /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar  
Source code for these samples is included on the ODP cluster at:
- /usr/odp/current/hadoop-client/src/hadoop-mapreduce-project/hadoop-mapreduce-example s
<br>

### **Testing the pi command**
To run the pi example with 16 maps and 100000 samples

```
yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar  pi 16 100000
```
### **Results**

```
21/10/21 13:13:32 INFO mapreduce.Job:  map 0% reduce 0%
21/10/21 13:13:40 INFO mapreduce.Job:  map 25% reduce 0%
21/10/21 13:13:41 INFO mapreduce.Job:  map 100% reduce 0%
21/10/21 13:13:45 INFO mapreduce.Job:  map 100% reduce 100%
21/10/21 13:13:46 INFO mapreduce.Job: Job job_1630864376208_4086 completed successfully
21/10/21 13:13:47 INFO mapreduce.Job: Counters: 54
        File System Counters
                FILE: Number of bytes read=358
                FILE: Number of bytes written=4480138
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=4294
                HDFS: Number of bytes written=215
                HDFS: Number of read operations=69
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=3
                HDFS: Number of bytes read erasure-coded=0
        Job Counters
                Launched map tasks=16
                Launched reduce tasks=1
                Data-local map tasks=16
                Total time spent by all maps in occupied slots (ms)=311910
                Total time spent by all reduces in occupied slots (ms)=9944
                Total time spent by all map tasks (ms)=103970
                Total time spent by all reduce tasks (ms)=2486
                Total vcore-milliseconds taken by all map tasks=103970
                Total vcore-milliseconds taken by all reduce tasks=2486
                Total megabyte-milliseconds taken by all map tasks=159697920
                Total megabyte-milliseconds taken by all reduce tasks=5091328
        Map-Reduce Framework
                Map input records=16
                Map output records=32
                Map output bytes=288
                Map output materialized bytes=448
                Input split bytes=2406
                Combine input records=0
                Combine output records=0
                Reduce input groups=2
                Reduce shuffle bytes=448
                Reduce input records=32
                Reduce output records=0
                Spilled Records=64
                Shuffled Maps =16
                Failed Shuffles=0
                Merged Map outputs=16
                GC time elapsed (ms)=2935
                CPU time spent (ms)=18350
                Physical memory (bytes) snapshot=18689650688
                Virtual memory (bytes) snapshot=58254319616
                Total committed heap usage (bytes)=19315818496
                Peak Map Physical memory (bytes)=1153404928
                Peak Map Virtual memory (bytes)=3401682944
                Peak Reduce Physical memory (bytes)=289771520
                Peak Reduce Virtual memory (bytes)=3877220352
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=1888
        File Output Format Counters
                Bytes Written=97
Job Finished in 24.143 seconds
Estimated value of Pi is 3.14157500000000000000
```

<br><br>

## 1.2 Run the wordcount example

- Connect to HADOOP cluster using SSH
```
> kinit
> Then insert Password : ||||||
```

- From the SSH session, use the following command to list samples  

Command
```
yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
```  
Results
```
[emile.ekane-ekane@hadoop-edge01 ~]$ yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
An example program must be given as the first argument.
Valid program names are:
  aggregatewordcount: An Aggregate based map/reduce program that counts the words in the input files.
  aggregatewordhist: An Aggregate based map/reduce program that computes the histogram of the words in the input files.
  bbp: A map/reduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.
  dbcount: An example job that count the pageview counts from a database.
  distbbp: A map/reduce program that uses a BBP-type formula to compute exact bits of Pi.
  grep: A map/reduce program that counts the matches of a regex in the input.
  join: A job that effects a join over sorted, equally partitioned datasets
  multifilewc: A job that counts words from several files.
  pentomino: A map/reduce tile laying program to find solutions to pentomino problems.
  pi: A map/reduce program that estimates Pi using a quasi-Monte Carlo method.
  randomtextwriter: A map/reduce program that writes 10GB of random textual data per node.
  randomwriter: A map/reduce program that writes 10GB of random data per node.
  secondarysort: An example defining a secondary sort to the reduce.
  sort: A map/reduce program that sorts the data written by the random writer.
  sudoku: A sudoku solver.
  teragen: Generate data for the terasort
  terasort: Run the terasort
  teravalidate: Checking results of terasort
  wordcount: A map/reduce program that counts the words in the input files.
  wordmean: A map/reduce program that counts the average length of the words in the input files.
  wordmedian: A map/reduce program that counts the median length of the words in the input files.
  wordstandarddeviation: A map/reduce program that counts the standard deviation of the length of the words in the input files.

```

- To get help on a specific sample , in this case wordcount sample:

```
yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
```

- Let's count all words in downloaded ebook ( in plain Text UTF-8)[Project Gutenberg](https://www.gutenberg.org/files/57333/57333-0.txt)

Let's download the book first

```
> wget https://www.gutenberg.org/files/57333/57333-0.txt
```
Copy the file to HDFS
```
> hdfs dfs -put text.txt /user/emile.ekane-ekane/
```
Finally let's count all words in the file using the command below :
```
> yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /user/emile.ekane-ekane/text.txt /user/emile.ekane-ekane/wordcount
```
Results
```

[emile.ekane-ekane@hadoop-edge01 ~]$ yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /user/emile.ekane-ekane/text.txt /user/emile.ekane-ekane/wordcount
21/10/21 13:48:59 INFO impl.TimelineReaderClientImpl: Initialized TimelineReader URI=https://hadoop-master03.efrei.online:8199/ws/v2/timeline/, clusterId=yarn-cluster
21/10/21 13:49:00 INFO client.AHSProxy: Connecting to Application History server at hadoop-master03.efrei.online/163.172.102.23:10200
21/10/21 13:49:00 INFO hdfs.DFSClient: Created token for emile.ekane-ekane: HDFS_DELEGATION_TOKEN owner=emile.ekane-ekane@EFREI.ONLINE, renewer=yarn, realUser=, issueDate=1634816940254, maxDate=1635421740254, sequenceNumber=6111, masterKeyId=64 on ha-hdfs:efrei
21/10/21 13:49:00 INFO security.TokenCache: Got dt for hdfs://efrei; Kind: HDFS_DELEGATION_TOKEN, Service: ha-hdfs:efrei, Ident: (token for emile.ekane-ekane: HDFS_DELEGATION_TOKEN owner=emile.ekane-ekane@EFREI.ONLINE, renewer=yarn, realUser=, issueDate=1634816940254, maxDate=1635421740254, sequenceNumber=6111, masterKeyId=64)
21/10/21 13:49:00 INFO client.ConfiguredRMFailoverProxyProvider: Failing over to rm2
21/10/21 13:49:00 INFO mapreduce.JobResourceUploader: Disabling Erasure Coding for path: /user/emile.ekane-ekane/.staging/job_1630864376208_4154
21/10/21 13:49:00 INFO input.FileInputFormat: Total input files to process : 1
21/10/21 13:49:00 INFO mapreduce.JobSubmitter: number of splits:1
21/10/21 13:49:01 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1630864376208_4154
21/10/21 13:49:01 INFO mapreduce.JobSubmitter: Executing with tokens: [Kind: HDFS_DELEGATION_TOKEN, Service: ha-hdfs:efrei, Ident: (token for emile.ekane-ekane: HDFS_DELEGATION_TOKEN owner=emile.ekane-ekane@EFREI.ONLINE, renewer=yarn, realUser=, issueDate=1634816940254, maxDate=1635421740254, sequenceNumber=6111, masterKeyId=64)]
21/10/21 13:49:01 INFO conf.Configuration: found resource resource-types.xml at file:/etc/hadoop/1.0.3.0-223/0/resource-types.xml
21/10/21 13:49:01 INFO impl.TimelineClientImpl: Timeline service address: hadoop-master03.efrei.online:8190
21/10/21 13:49:01 INFO impl.YarnClientImpl: Submitted application application_1630864376208_4154
21/10/21 13:49:01 INFO mapreduce.Job: The url to track the job: https://hadoop-master02.efrei.online:8090/proxy/application_1630864376208_4154/
21/10/21 13:49:01 INFO mapreduce.Job: Running job: job_1630864376208_4154
21/10/21 13:49:11 INFO mapreduce.Job: Job job_1630864376208_4154 running in uber mode : false
21/10/21 13:49:11 INFO mapreduce.Job:  map 0% reduce 0%
21/10/21 13:49:20 INFO mapreduce.Job:  map 100% reduce 0%
21/10/21 13:49:29 INFO mapreduce.Job:  map 100% reduce 100%
21/10/21 13:49:30 INFO mapreduce.Job: Job job_1630864376208_4154 completed successfully
21/10/21 13:49:30 INFO mapreduce.Job: Counters: 54
        File System Counters
                FILE: Number of bytes read=205052
                FILE: Number of bytes written=936369
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=798883
                HDFS: Number of bytes written=151939
                HDFS: Number of read operations=8
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=2
                HDFS: Number of bytes read erasure-coded=0
        Job Counters
                Launched map tasks=1
                Launched reduce tasks=1
                Data-local map tasks=1
                Total time spent by all maps in occupied slots (ms)=18603
                Total time spent by all reduces in occupied slots (ms)=25972
                Total time spent by all map tasks (ms)=6201
                Total time spent by all reduce tasks (ms)=6493
                Total vcore-milliseconds taken by all map tasks=6201
                Total vcore-milliseconds taken by all reduce tasks=6493
                Total megabyte-milliseconds taken by all map tasks=9524736
                Total megabyte-milliseconds taken by all reduce tasks=13297664
        Map-Reduce Framework
                Map input records=14579
                Map output records=124749
                Map output bytes=1210303
                Map output materialized bytes=205052
                Input split bytes=109
                Combine input records=124749
                Combine output records=13644
                Reduce input groups=13644
                Reduce shuffle bytes=205052
                Reduce input records=13644
                Reduce output records=13644
                Spilled Records=27288
                Shuffled Maps =1
                Failed Shuffles=0
                Merged Map outputs=1
                GC time elapsed (ms)=216
                CPU time spent (ms)=6690
                Physical memory (bytes) snapshot=1478795264
                Virtual memory (bytes) snapshot=7296086016
                Total committed heap usage (bytes)=1496842240
                Peak Map Physical memory (bytes)=1177706496
                Peak Map Virtual memory (bytes)=3411832832
                Peak Reduce Physical memory (bytes)=301088768
                Peak Reduce Virtual memory (bytes)=3884253184
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=798774
        File Output Format Counters
                Bytes Written=151939

```

- Let's view the ouput of the job

```
> hdfs dfs -cat/user/emile.ekane-ekane/wordcount/part-r-00000
```
This command concatenates all the output files produced by the job. It
displays the output to the console. The output is similar to the following
text:
```
trying  6
tumult  3
turn    22
turn,   3
```
Each line represents a word and how many times it occurred in the input
data.

<br><br>


## 1.3 The Sudoku example
[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids. Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells. The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells. So our input should be a file that is in the following format:
- Nine rows of nine columns
- Each column can contain either a number or ` ? ` (which indicates a blank cell)
- Cells are separated by a space  

There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.  

Let's create a file called sudoku.dta
```
> Cat > sudoku.dta
And paste this in it :
8 5 ? 3 9 ? ? ? ?
? ? 2 ? ? ? ? ? ?
? ? 6 ? 1 ? ? ? 2
? ? 4 ? ? 3 ? 5 9
? ? 8 9 ? 1 4 ? ?
3 2 ? 4 ? ? 8 ? ?
9 ? ? ? 8 ? 5 ? ?
? ? ? ? ? ? 2 ? ?
? ? ? ? 4 5 ? 7 8

Let's copy the file to our HDFS local 
> hdfs dfs -put sudoku.dta /user/emile.ekane-ekane/
```
Let's run this example problem through the Sudoku example, use the following command:
```
> yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar  sudoku sudoku.dta
```
The results we obtain :

```
[emile.ekane-ekane@hadoop-edge01 ~]$ yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar  sudoku sudoku.dta
Solving sudoku.dta
8 5 1 3 9 2 6 4 7
4 3 2 6 7 8 1 9 5
7 9 6 5 1 4 3 8 2
6 1 4 8 2 3 7 5 9
5 7 8 9 6 1 4 2 3
3 2 9 4 5 7 8 1 6
9 4 7 2 8 6 5 3 1
1 8 5 7 3 9 2 6 4
2 6 3 1 4 5 9 7 8

Found 1 solutions
```

<br><br>

## 1.4 Pi example
The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the
value of pi. Points are placed at random in a unit square.  
The square also contains a circle. The probability that the points fall within the circle is equal to the area of the circle, pi/4.  
The value of pi can be estimated from the value of 4R. R is the ratio of the number of points that are inside the circle to the total number of points that
are within the square.  
The larger the sample of points used, the better the estimate is.  
<br>
Use the following command to run this sample. This command uses 16 maps
with 10,000,000 samples each to estimate the value of pi:  

```
> yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar  pi 16 1000000
```
The value returned by this command is similar to **3.14159155000000000000**. For
references, the first 10 decimal places of pi are 3.1415926535.

<br><br>

## 1.5 10 GB GraySort example

- Generate 10GB of data, which is stored in our home directory at /user/<username>/data/10GB-sort-input:

```
> yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar  teragen -Dmapred.map.tasks=50 100000000 /user/emile.ekane-ekane/data/10GB-sort-input
```
The -Dmapred.map.tasks tells Hadoop how many map tasks to use for this job. The final two parameters instruct the job to create 10 GB of data and to store it at /example/data/10GB-sort-input

- The following command to sort the data
```
> yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /user/emile.ekane-ekane/data/10GB-sort-input /user/emile.ekane-ekane/data/10GB-sort-output
```
The -Dmapred.reduce.tasks tells Hadoop how many reduce tasks to use for
the job. The final two parameters are just the input and output locations
for data.
- The following command to validate the data generated
```
> yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /user/emile.ekane-ekane/data/10GB-sort-output /user/emile.ekane-ekane/data/10GB-sort-validate
```







<br><br>

# 2 MapReduce2
In this tutorial I will describe how to write a simple MapReduce program for Hadoop using Python programming language
<br><br>

## 2.1 Motivation
Even though the Hadoop framework is written in Java, programs for Hadoop
need not to be coded in Java but can also be developed in other languages like
Python or C++ (the latter since version 0.14.1).  
However, Hadoop’s documentation and the most prominent Python example
on the Hadoop website could make you think that you must translate your
Python code using Jython into a Java jar file.  
Obviously, this is not very convenient and can even be problematic if you depend on Python features not provided by Jython


<br><br>

## 2.2 What we want to do
We will write a simple MapReduce program (see also the MapReduce article on Wikipedia) for Hadoop in Python but without using Jython to translate our code to Java jar files.  
Our program will mimick the WordCount, i.e. it reads text files and counts how often words occur. The input is text files and the output is text files, each line of which contains a word and the count ofhow often it occured, separated by a tab.  
*Note: You can also use programming languages other than Python such as Perl or Ruby with the "technique" described in this tutorial.*
<br><br>

## 2.3 Python MapReduce Code

<br>

### 2.3.1 Map step: Mapper.py
We will save the following code in /user/emile.ekane-ekane/mapper.py  
It will read data from STDIN, split it into words and output a listy of lines mapping words to their (intermediate) counts to STDOUT.

```
> cat > mapper.py
```

The **_Mapper.py_** code
```
#!/ usr/bin/env python
""" mapper .py """
import sys
# input comes from STDIN ( standard input )
for line in sys.stdin :
    # remove leading and trailing whitespace
    # @TODO
    line = line.strip()
    # split the line into words
    # @TODO
    words = line.split()
    
    # increase counters
    for word in words :
        # write the results to STDOUT ( standard output );
        # what we output here will be the input for the
        # Reduce step , i.e. the input for reducer.py
        # 
        #tab - delimited ; the trivial word count is 1
        # @TODO
        print '%s \t%s' % (word, 1)
```
To make sure our file have the execution permission , we run the ``ls -l mapper.py`` to see the permissions, then grant execution permission with this trick ``` chmod +x /home/emile.ekane-ekane/mapper.py```
<br><br><br>

### 2.3.2 Reduce step: reducer.py

Save the following code in the file /home/<username>/reducer.py.
It will read the results of mapper.py from STDIN (so the output format of
mapper.py and the expected input format of reducer.py must match) and
sum the occurrences of each word to a final count, and then output its results
to STDOUT.

The **_Reducer.py_** code
```
#!/usr/bin/env python
"""reducer.py"""

from operator import itemgetter
import sys

current_word = None
current_count = 0
word = None

# input comes from STDIN
for line in sys.stdin :
    # remove leading and trailing white space
    # @TODO
    line = line.strip()

    # parse the input we got from mapper.py
    # @TODO
    word, count = line.split('\t', 1)

    # convert count ( currently a string) to int
    # @TODO
    try:
        count = int(count)
    except ValueError:
        # count was not a number, so silently
        # ignore/discard this line
        continue

    # this IF=switch only works because Hadoop sorts map output
    # by key ( here : word ) before it is passed to the reducer
    # @TODO
    if current_word == word:
        current_count += count
    else:
        if current_word:
            # write result to STDOUT
            print '%s\t%s' % (current_word, current_count)
        current_count = count
        current_word = word

    # do not forget to output the last word if needed !
    # @TODO
if current_word == word:
        print '%s\t%s' % (current_word, current_count)
```
To make sure our file have the execution permission , we run the ``ls -l reducer.py`` to see the permissions, then grant execution permission with this trick ``` chmod +x /home/emile.ekane-ekane/reducer.py```
<br><br><br>


### 2.3.3 Test your code (cat data | map | sort | reduce)
Let's test your mapper.py and reducer.py scripts locally before using them in a MapReduce job.
```
> echo "foo foo quux labs foo bar quux" | /home/emile.ekane-ekane/mapper.py
foo      1
foo      1
quux     1
labs     1
foo      1
bar      1
quux     1

> echo "foo foo quux labs foo bar quux" | /home/emile.ekane-ekane/mapper.py | sort -k1,1 | /home/emile.ekane-ekane/reducer.py
y
bar     1
foo     3
labs    1
quux    2
```
Using a downloaded Ebook
```
> cat text.txt | /home/emile.ekane-ekane/mapper.py
# After we reduce
>  cat text.txt | /home/emile.ekane-ekane/mapper.py | sort -k1,1 | /home/emile.ekane-ekane/reducer.py

```


<br><br><br>

## 2.4 Running the Python Code on Hadoop

### 2.4.1 Download example input data
We wil use three ebooks form Project Gutenberg for this :
- The Outline of Science, Vol. 1 (of 4) by J. Arthur Thomson; [download](https://www.gutenberg.org/cache/epub/20417/pg20417.txt)
- The Notebooks of Leonardo Da Vinci; [download](https://www.gutenberg.org/files/5000/5000-8.txt) 
- Ulysses by James Joyce; [download](https://www.gutenberg.org/files/4300/4300-0.txt) 
Download each ebook as text files in Plain Text UTF-8 encoding and store the files in your home directory
```
wget https://www.gutenberg.org/cache/epub/20417/pg20417.txt
wget https://www.gutenberg.org/files/5000/5000-8.txt
wget https://www.gutenberg.org/files/4300/4300-0.txt

#Rename the files
mv pg20417.txt outline.txt
mv 5000-8.txt vinci.txt
mv 4300-0.txt ulysse.txt
```
<br><br>

### 2.4.2 Copy local example data to HDFS
Before we run the actual MapReduce job, we must first copy the files from our local file system to Hadoop’s HDFS
```
hdfs dfs -put outline.txt vinci.txt ulysse.txt
    #OR 
hdfs dfs -copyFromLocal outline.txt vinci.txt ulysse.txt
```
<br><br>

### 2.4.3 Run the MapReduce job
Now that everything is prepared, we can finally run our Python MapReduce job on the Hadoop cluster.
The job will read all the files in the HDFS directory /user/<username>/gutenberg, process it, and store the results in the HDFS directory /user/<username>/gutenberg-output
```
> hdfs dfs -mkdir /user/emile.ekane-ekane/gutenberg

#Move the files in the directory

[emile.ekane-ekane@hadoop-edge01 ~]$ hdfs dfs -ls /user/emile.ekane-ekane/gutenberg
Found 3 items
-rw-r--r--   3 emile.ekane-ekane emile.ekane-ekane     674570 2021-10-24 18:43 /user/emile.ekane-ekane/gutenberg/outline.txt
-rw-r--r--   3 emile.ekane-ekane emile.ekane-ekane    1586336 2021-10-24 18:45 /user/emile.ekane-ekane/gutenberg/ulysse.txt
-rw-r--r--   3 emile.ekane-ekane emile.ekane-ekane    1428843 2021-10-24 18:45 /user/emile.ekane-ekane/gutenberg/vinci.txt

# We run the Map Reduce job
> yarn jar /usr/odp/current/hadoop-mapreduce-client/hadoop-streaming.jar -input /user/emile.ekane-ekane/gutenberg/* -output /user/emile.ekane-ekane/gutenberg-output -file /home/emile.ekane-ekane/mapper.py -mapper /home/emile.ekane-ekane/mapper.py -file /home/emile.ekane-ekane/reducer.py -reducer /home/emile.ekane-ekane/reducer.py


Results

[emile.ekane-ekane@hadoop-edge01 ~]$ hdfs dfs -ls /user/emile.ekane-ekane/gutenberg-output/
Found 2 items
-rw-r--r--   3 emile.ekane-ekane emile.ekane-ekane          0 2021-10-27 08:26 /user/emile.ekane-ekane/gutenberg-output/_SUCCESS
-rw-r--r--   3 emile.ekane-ekane emile.ekane-ekane     887415 2021-10-27 08:26 /user/emile.ekane-ekane/gutenberg-output/part-00000

```
Explanations
- The first line hadoop jar /usr/lib/hadoop/hadoop-streaming.jar is launching Hadoop with the Hadoop Streaming jar. A jar is a Java Archive file, and Hadoop Streaming is a special kind of jar that allows you to run non Java programs.
- The lines -file /home/emile.ekane-ekane/mapper.py,/home/emile.ekane-ekane/reducer.py tells Hadoop that it needs to "ship" the executable mapper and reducer scripts to every node on the cluster. If you are working on the master node, these files need to be on your master (remote) filesystem. Remember, these files do not exist before the job is run, so you need to package those files with the job so they run
- The line -input [[input-file]] tells the job where your source file(s) are. These files need to be either in HDFS or S3. If you specify a directory, all files in the directory will be used as inputs
- The line line -output [[output-location]] tells the job where to store the output of the job, either in HDFS or S3. This parameter is just a name of a location, and it must not exist before running the job otherwise the job will fail.
- The line -mapper basic-mapper.py specifies the name of the executable for the mapper. Note that you need to ship the programs if they are custom programs
- The line -reducer reducer.py specifies the name of the executable for the mapper. Note that you need to ship the programs if they are custom programs

<br><br>

### 2.4.4 Improved Mapper and Reducer code: using Python iterators and generators
Generally speaking, iterators and generators (functions that create iterators,
for example with Python’s yield statement) have the advantage that an element of a sequence is not produced until you actually need it.  


This can help a lot in terms of computational expensiveness or memory consumption depending on the task at hand.    


*Note: The following Map and Reduce scripts will only work "correctly" when
being run in the Hadoop context, i.e. as Mapper and Reducer in a MapReduce
job. This means that running the naive test command "cat DATA j ./mapper.py
j sort -k1,1 j ./reducer.py" will not work correctly anymore because some functionality is intentionally outsourced to Hadoop.*  


Precisely, we compute the sum of a word’s occurrences, e.g. ("foo", 4), only
if by chance the same word (foo) appears multiple times in succession.
In the majority of cases, however, we let the Hadoop group the (key, value)
pairs between the Map and the Reduce step because Hadoop is more efficient
in this regard than our simple Python scripts. 
<br><br>


### 2.4.5 Mapper.py

```
#!/usr/bin/env python
"""A more advanced Mapper, using Python iterators and generators."""

import sys

def read_input(file):
    for line in file:
        # split the line into words
        yield line.split()

def main(separator='\t'):
    # input comes from STDIN (standard input)
    data = read_input(sys.stdin)
    for words in data:
        # write the results to STDOUT (standard output);
        # what we output here will be the input for the
        # Reduce step, i.e. the input for reducer.py
        #
        # tab-delimited; the trivial word count is 1
        for word in words:
            print '%s\t%s' % (word, 1)

if __name__ == "__main__":
    main()
```

### 2.4.6 Reducer.py

```
#!/usr/bin/env python
"""A more advanced Reducer, using Python iterators and generators."""

from itertools import groupby
from operator import itemgetter
import sys

def read_mapper_output(file, separator='\t'):
    for line in file:
        yield line.rstrip().split(separator, 1)

def main(separator='\t'):
    # input comes from STDIN (standard input)
    data = read_mapper_output(sys.stdin, separator=separator)
    # groupby groups multiple word-count pairs by word,
    # and creates an iterator that returns consecutive keys and their group:
    #   current_word - string containing a word (the key)
    #   group - iterator yielding all ["&lt;current_word&gt;", "&lt;count&gt;"] items
    for current_word, group in groupby(data, itemgetter(0)):
        try:
            total_count = sum(int(count) for current_word, count in group)
            print "%s%s%d" % (current_word, separator, total_count)
        except ValueError:
            # count was not a number, so silently discard this item
            pass

if __name__ == "__main__":
    main()
```


<br><br><br><br>
*Updated the 27/10/2021*  
*By [Emile](http://ekane3.github.io)*