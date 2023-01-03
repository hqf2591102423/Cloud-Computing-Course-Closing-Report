[huangqifa@hadoop4 movie]$ chmod +x run.sh 
[huangqifa@hadoop4 movie]$ chmod +x map_new.py red_new.py 
sudo gedit run.sh
编辑为如下

HADOOP_CMD="/usr/local/hadoop/bin/hadoop"
STREAM_JAR_PATH="/usr/local/hadoop/share/hadoop/tools/lib/hadoop-streaming-2.7.7.jar"

INPUT_FILE_PATH_1="/The_Man_of_Property.txt"
OUTPUT_PATH="/output"

$HADOOP_CMD fs -rmr -skipTrash $OUTPUT_PATH

# Step 1.
$HADOOP_CMD jar $STREAM_JAR_PATH \
    -input $INPUT_FILE_PATH_1 \
    -output $OUTPUT_PATH \
    -mapper "python map_new.py" \
    -reducer "python red_new.py" \
    -file ./map_new.py \
    -file ./red_new.py

[huangqifa@hadoop4 movie]$ hdfs dfs -put /home/huangqifa/movie/The_Man_of_Property.txt /
[huangqifa@hadoop4 movie]$ ./run.sh 
rmr: DEPRECATED: Please use 'rm -r' instead.
rmr: `/output': No such file or directory
22/12/07 16:20:40 WARN streaming.StreamJob: -file option is deprecated, please use generic option -files instead.
packageJobJar: [./map_new.py, ./red_new.py, /tmp/hadoop-unjar4840988545769026232/] [] /tmp/streamjob4543185587218023201.jar tmpDir=null
22/12/07 16:20:41 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
22/12/07 16:20:41 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
22/12/07 16:20:43 INFO mapred.FileInputFormat: Total input paths to process : 1
22/12/07 16:20:43 INFO mapreduce.JobSubmitter: number of splits:2
22/12/07 16:20:43 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1670400976288_0002
22/12/07 16:20:44 INFO impl.YarnClientImpl: Submitted application application_1670400976288_0002
22/12/07 16:20:44 INFO mapreduce.Job: The url to track the job: http://hadoop4:8088/proxy/application_1670400976288_0002/
22/12/07 16:20:44 INFO mapreduce.Job: Running job: job_1670400976288_0002
22/12/07 16:20:56 INFO mapreduce.Job: Job job_1670400976288_0002 running in uber mode : false
22/12/07 16:20:56 INFO mapreduce.Job:  map 0% reduce 0%
22/12/07 16:21:08 INFO mapreduce.Job:  map 100% reduce 0%
22/12/07 16:21:15 INFO mapreduce.Job:  map 100% reduce 100%
22/12/07 16:21:16 INFO mapreduce.Job: Job job_1670400976288_0002 completed successfully
22/12/07 16:21:16 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=1076619
		FILE: Number of bytes written=2531285
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=636497
		HDFS: Number of bytes written=181530
		HDFS: Number of read operations=9
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=2
	Job Counters 
		Launched map tasks=2
		Launched reduce tasks=1
		Data-local map tasks=2
		Total time spent by all maps in occupied slots (ms)=18391
		Total time spent by all reduces in occupied slots (ms)=4075
		Total time spent by all map tasks (ms)=18391
		Total time spent by all reduce tasks (ms)=4075
		Total vcore-milliseconds taken by all map tasks=18391
		Total vcore-milliseconds taken by all reduce tasks=4075
		Total megabyte-milliseconds taken by all map tasks=18832384
		Total megabyte-milliseconds taken by all reduce tasks=4172800
	Map-Reduce Framework
		Map input records=2866
		Map output records=111818
		Map output bytes=852977
		Map output materialized bytes=1076625
		Input split bytes=190
		Combine input records=0
		Combine output records=0
		Reduce input groups=16985
		Reduce shuffle bytes=1076625
		Reduce input records=111818
		Reduce output records=16984
		Spilled Records=223636
		Shuffled Maps =2
		Failed Shuffles=0
		Merged Map outputs=2
		GC time elapsed (ms)=368
		CPU time spent (ms)=6730
		Physical memory (bytes) snapshot=668762112
		Virtual memory (bytes) snapshot=6364340224
		Total committed heap usage (bytes)=467140608
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=636307
	File Output Format Counters 
		Bytes Written=181530
22/12/07 16:21:16 INFO streaming.StreamJob: Output directory: /output
[huangqifa@hadoop4 movie]$ 

[huangqifa@hadoop4 movie]$ hdfs dfs -cat /output/*

“what’s	1
“white	1
“who	1
“will	2
“women	1
“wouldn’t	1
“you	16
“your	1
“you’d	2
“you’ll	1
“you’ve	1
“‘of	1
”	34
[huangqifa@hadoop4 movie]$ 






