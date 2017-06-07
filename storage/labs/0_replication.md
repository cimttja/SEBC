[ec2-user@ip-172-31-16-170 ~]$ sudo -i
[root@ip-172-31-16-170 ~]# mkdir -p /usr/local/hadoop
[root@ip-172-31-16-170 ~]# cp /opt/cloudera/parcels/CDH-5.8.3-1.cdh5.8.3.p0.2/jars/hadoop- /usr/local/hadoop/hadoop-test-2.6.0-mr1-cdh5.8.3.jar
[root@ip-172-31-16-170 ~]# cp /opt/cloudera/parcels/CDH-5.8.3-1.cdh5.8.3.p0.2/jars/hadoop-examples.jar /usr/local/hadoop/hadoop-examples.jar
[root@ip-172-31-16-170 ~]# cd /usr/local/hadoop
[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hadoop jar hadoop-test-2.6.0-mr1-cdh5.8.3.jar TestDFSIO -write -nrFiles 10 -fileSize 1000
	17/06/07 08:56:15 INFO fs.TestDFSIO: TestDFSIO.1.7
	17/06/07 08:56:15 INFO fs.TestDFSIO: nrFiles = 10
	17/06/07 08:56:15 INFO fs.TestDFSIO: nrBytes (MB) = 1000.0
	17/06/07 08:56:15 INFO fs.TestDFSIO: bufferSize = 1000000
	17/06/07 08:56:15 INFO fs.TestDFSIO: baseDir = /benchmarks/TestDFSIO
	17/06/07 08:56:16 INFO fs.TestDFSIO: creating control file: 1048576000 bytes, 10 files
	17/06/07 08:56:17 INFO fs.TestDFSIO: created control files for: 10 files
	17/06/07 08:56:17 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-28-243.eu-central-1.compute.internal/172.31.28.243:8032
	17/06/07 08:56:17 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-28-243.eu-central-1.compute.internal/172.31.28.243:8032
	17/06/07 08:56:17 INFO mapred.FileInputFormat: Total input paths to process : 10
	17/06/07 08:56:17 INFO mapreduce.JobSubmitter: number of splits:10
	17/06/07 08:56:17 INFO Configuration.deprecation: dfs.https.address is deprecated. Instead, use dfs.namenode.https-address
	17/06/07 08:56:17 INFO Configuration.deprecation: io.bytes.per.checksum is deprecated. Instead, use dfs.bytes-per-checksum
	17/06/07 08:56:18 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1496831851286_0001
	17/06/07 08:56:18 INFO impl.YarnClientImpl: Submitted application application_1496831851286_0001
	17/06/07 08:56:18 INFO mapreduce.Job: The url to track the job: http://ip-172-31-28-243.eu-central-1.compute.internal:8088/proxy/application_1496831851286_0001/
	17/06/07 08:56:18 INFO mapreduce.Job: Running job: job_1496831851286_0001
	17/06/07 08:56:25 INFO mapreduce.Job: Job job_1496831851286_0001 running in uber mode : false
	17/06/07 08:56:25 INFO mapreduce.Job:  map 0% reduce 0%
	.
	.
	.
[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hadoop jar hadoop-test-2.6.0-mr1-cdh5.8.3.jar TestDFSIO -write -nrFiles
	17/06/07 08:56:15 INFO fs.TestDFSIO: TestDFSIO.1.7
	17/06/07 08:56:15 INFO fs.TestDFSIO: nrFiles = 10
	17/06/07 08:56:15 INFO fs.TestDFSIO: nrBytes (MB) = 1000.0
	17/06/07 08:56:15 INFO fs.TestDFSIO: bufferSize = 1000000
	17/06/07 08:56:15 INFO fs.TestDFSIO: baseDir = /benchmarks/TestDFSIO
	17/06/07 08:56:16 INFO fs.TestDFSIO: creating control file: 1048576000 bytes, 10 files
	17/06/07 08:56:17 INFO fs.TestDFSIO: created control files for: 10 files
	17/06/07 08:56:17 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-28-243.eu-central-1.compute.interna
	17/06/07 08:56:17 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-28-243.eu-central-1.compute.interna
	17/06/07 08:56:17 INFO mapred.FileInputFormat: Total input paths to process : 10
	17/06/07 08:56:17 INFO mapreduce.JobSubmitter: number of splits:10
	17/06/07 08:56:17 INFO Configuration.deprecation: dfs.https.address is deprecated. Instead, use dfs.namenode.https-ad
	17/06/07 08:56:17 INFO Configuration.deprecation: 
	.
	.
	.
[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hdfs dfs -mkdir /user/mstcimt
[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hadoop jar hadoop-*examples*.jar teragen 5000000 /user/cimttja
	17/06/07 09:13:22 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-28-243.eu-central-1.compute.internal/172.31.28.243:8032
	17/06/07 09:13:22 INFO terasort.TeraSort: Generating 5000000 using 2
	17/06/07 09:13:22 INFO mapreduce.JobSubmitter: number of splits:2
	17/06/07 09:13:23 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1496831851286_0003
	17/06/07 09:13:23 INFO impl.YarnClientImpl: Submitted application application_1496831851286_0003
	17/06/07 09:13:23 INFO mapreduce.Job: The url to track the job: http://ip-172-31-28-243.eu-central-1.compute.internal:8088/proxy/application_1496831851286_0003/
	17/06/07 09:13:23 INFO mapreduce.Job: Running job: job_1496831851286_0003
	.
	.
	.

[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hadoop distcp hdfs://ip-172-31-28-243.eu-central-1.compute.internal:8020/user/cimttja hdfs://ip-172-31-28-243.eu-central-1.compute.internal:8020/user/mstcimt
17/06/07 10:00:50 INFO tools.DistCp: Input Options: DistCpOptions{atomicCommit=false, syncFolder=false, deleteMissing=false, ignoreFailures=false, overwrite=false, skipCRC=false, blocking=true, numListstatusThreads=0, maxMaps=20, mapBandwidth=100, sslConfigurationFile='null', copyStrategy='uniformsize', preserveStatus=[], preserveRawXattrs=false, atomicWorkPath=null, logPath=null, sourceFileListing=null, sourcePaths=[hdfs://ip-172-31-28-243.eu-central-1.compute.internal:8020/user/cimttja], targetPath=hdfs://ip-172-31-28-243.eu-central-1.compute.internal:8020/user/mstcimt, targetPathExists=true, filtersFile='null'}
17/06/07 10:00:50 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-28-243.eu-central-1.compute.internal/172.31.28.243:8032
17/06/07 10:00:51 INFO tools.SimpleCopyListing: Paths (files+dirs) cnt = 4; dirCnt = 1
17/06/07 10:00:51 INFO tools.SimpleCopyListing: Build file listing completed.
17/06/07 10:00:51 INFO Configuration.deprecation: io.sort.mb is deprecated. Instead, use mapreduce.task.io.sort.mb
17/06/07 10:00:51 INFO Configuration.deprecation: io.sort.factor is deprecated. Instead, use mapreduce.task.io.sort.factor
17/06/07 10:00:51 INFO tools.DistCp: Number of paths in the copy list: 4
17/06/07 10:00:51 INFO tools.DistCp: Number of paths in the copy list: 4
17/06/07 10:00:51 INFO client.RMProxy: Connecting to ResourceManager at ip-172-31-28-243.eu-central-1.compute.internal/172.31.28.243:8032
17/06/07 10:00:51 INFO mapreduce.JobSubmitter: number of splits:3
17/06/07 10:00:52 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1496842591201_0001
17/06/07 10:00:52 INFO impl.YarnClientImpl: Submitted application application_1496842591201_0001
17/06/07 10:00:52 INFO mapreduce.Job: The url to track the job: http://ip-172-31-28-243.eu-central-1.compute.internal:8088/proxy/application_1496842591201_0001/
17/06/07 10:00:52 INFO tools.DistCp: DistCp job-id: job_1496842591201_0001
17/06/07 10:00:52 INFO mapreduce.Job: Running job: job_1496842591201_0001
17/06/07 10:00:59 INFO mapreduce.Job: Job job_1496842591201_0001 running in uber mode : false
17/06/07 10:00:59 INFO mapreduce.Job:  map 0% reduce 0%
17/06/07 10:01:05 INFO mapreduce.Job:  map 33% reduce 0%
17/06/07 10:01:09 INFO mapreduce.Job:  map 100% reduce 0%
17/06/07 10:01:09 INFO mapreduce.Job: Job job_1496842591201_0001 completed successfully
17/06/07 10:01:09 INFO mapreduce.Job: Counters: 33
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=375120
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=500001798
                HDFS: Number of bytes written=500000000
                HDFS: Number of read operations=57
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=13
        Job Counters
                Launched map tasks=3
                Other local map tasks=3
                Total time spent by all maps in occupied slots (ms)=19208
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=19208
                Total vcore-seconds taken by all map tasks=19208
                Total megabyte-seconds taken by all map tasks=19668992
        Map-Reduce Framework
                Map input records=4
                Map output records=0
                Input split bytes=342
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=163
                CPU time spent (ms)=11570
                Physical memory (bytes) snapshot=665489408
                Virtual memory (bytes) snapshot=4736065536
                Total committed heap usage (bytes)=1050148864
        File Input Format Counters
                Bytes Read=1456
        File Output Format Counters
                Bytes Written=0
        org.apache.hadoop.tools.mapred.CopyMapper$Counter
                BYTESCOPIED=500000000
                BYTESEXPECTED=500000000
                COPY=4
[root@ip-172-31-16-170 hadoop]# hdfs fsck /user/origin/ -files -blocks
Connecting to namenode via http://ip-172-31-28-243.eu-central-1.compute.internal:50070
FSCK started by root (auth:SIMPLE) from /172.31.16.170 for path /user/origin/ at Wed Jun 07 10:24:29 EDT 2017
/user/origin/ <dir>
/user/origin/_SUCCESS 0 bytes, 0 block(s):  OK

/user/origin/part-m-00000 250000000 bytes, 2 block(s):  OK
0. BP-1757816971-172.31.28.243-1496830389511:blk_1073742941_2117 len=134217728 Live_repl=3
1. BP-1757816971-172.31.28.243-1496830389511:blk_1073742943_2119 len=115782272 Live_repl=3

/user/origin/part-m-00001 250000000 bytes, 2 block(s):  OK
0. BP-1757816971-172.31.28.243-1496830389511:blk_1073742940_2116 len=134217728 Live_repl=3
1. BP-1757816971-172.31.28.243-1496830389511:blk_1073742942_2118 len=115782272 Live_repl=3

Status: HEALTHY
 Total size:    500000000 B
 Total dirs:    1
 Total files:   3
 Total symlinks:                0
 Total blocks (validated):      4 (avg. block size 125000000 B)
 Minimally replicated blocks:   4 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          5
 Number of racks:               1
FSCK ended at Wed Jun 07 10:24:29 EDT 2017 in 3 milliseconds


The filesystem under path '/user/origin/' is HEALTHY
[root@ip-172-31-16-170 hadoop]# hdfs fsck /user/target/ -files -blocks
Connecting to namenode via http://ip-172-31-28-243.eu-central-1.compute.internal:50070
FSCK started by root (auth:SIMPLE) from /172.31.16.170 for path /user/target/ at Wed Jun 07 10:24:51 EDT 2017
/user/target/ <dir>
/user/target/origin <dir>
/user/target/origin/_SUCCESS 0 bytes, 0 block(s):  OK

/user/target/origin/part-m-00000 250000000 bytes, 2 block(s):  OK
0. BP-1757816971-172.31.28.243-1496830389511:blk_1073742962_2138 len=134217728 Live_repl=3
1. BP-1757816971-172.31.28.243-1496830389511:blk_1073742963_2139 len=115782272 Live_repl=3

/user/target/origin/part-m-00001 250000000 bytes, 2 block(s):  OK
0. BP-1757816971-172.31.28.243-1496830389511:blk_1073742965_2141 len=134217728 Live_repl=3
1. BP-1757816971-172.31.28.243-1496830389511:blk_1073742966_2142 len=115782272 Live_repl=3

Status: HEALTHY
 Total size:    500000000 B
 Total dirs:    2
 Total files:   3
 Total symlinks:                0
 Total blocks (validated):      4 (avg. block size 125000000 B)
 Minimally replicated blocks:   4 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          5
 Number of racks:               1
FSCK ended at Wed Jun 07 10:24:51 EDT 2017 in 2 milliseconds


The filesystem under path '/user/target/' is HEALTHY
