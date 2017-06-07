[ec2-user@ip-172-31-16-170 /]$ sudo -i
[root@ip-172-31-16-170 ~]# useradd cimttja
[root@ip-172-31-16-170 ~]# usermod cimttja -aG wheel
[root@ip-172-31-16-170 ~]# usermod cimttja -aG ec2-user
[root@ip-172-31-16-170 ~]# usermod cimttja -aG adm
[root@ip-172-31-16-170 ~]# usermod cimttja -aG wheel
[root@ip-172-31-16-170 ~]# usermod cimttja -aG systemd-journal
[root@ip-172-31-16-170 ~]# sudo -su hdfs hdfs dfs -mkdir /user/cimttja
[root@ip-172-31-16-170 ~]# sudo -su hdfs hdfs dfs -chown -R cimttja:cimttja /user/cimttja
[root@ip-172-31-16-170 ~]# exit
[root@ip-172-31-16-170 hadoop]# sudo -su cimttja hadoop jar hadoop-*examples*.jar teragen  -Ddfs.block.size=33554432  100000000 /user/cimttja/data
[root@ip-172-31-16-170 hadoop]#  sudo -su cimttja time hadoop jar hadoop-*examples*.jar teragen  -Ddfs.block.size=33554432  100000000 /user/cimttja/data2
17/06/07 10:51:05 INFO mapreduce.Job:  map 94% reduce 0%
17/06/07 10:51:07 INFO mapreduce.Job:  map 95% reduce 0%
17/06/07 10:51:08 INFO mapreduce.Job:  map 97% reduce 0%
17/06/07 10:51:11 INFO mapreduce.Job:  map 99% reduce 0%
17/06/07 10:51:12 INFO mapreduce.Job:  map 100% reduce 0%
17/06/07 10:51:12 INFO mapreduce.Job: Job job_1496842591201_0005 completed successfully
17/06/07 10:51:12 INFO mapreduce.Job: Counters: 31
        File System Counters
                FILE: Number of bytes read=0
                FILE: Number of bytes written=244320
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=170
                HDFS: Number of bytes written=10000000000
                HDFS: Number of read operations=8
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=4
        Job Counters
                Launched map tasks=2
                Other local map tasks=2
                Total time spent by all maps in occupied slots (ms)=293405
                Total time spent by all reduces in occupied slots (ms)=0
                Total time spent by all map tasks (ms)=293405
                Total vcore-seconds taken by all map tasks=293405
                Total megabyte-seconds taken by all map tasks=300446720
        Map-Reduce Framework
                Map input records=100000000
                Map output records=100000000
                Input split bytes=170
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=1256
                CPU time spent (ms)=142750
                Physical memory (bytes) snapshot=363438080
                Virtual memory (bytes) snapshot=3174137856
                Total committed heap usage (bytes)=429916160
        org.apache.hadoop.examples.terasort.TeraGen$Counters
                CHECKSUM=214760662691937609
        File Input Format Counters
                Bytes Read=0
        File Output Format Counters
                Bytes Written=10000000000

real    2m41.025s
user    0m6.239s
sys     0m0.285s
[root@ip-172-31-16-170 hadoop]#  sudo -su cimttja time hadoop jar hadoop-*examples*.jar terasort /user/cimttja/data2 /user/cimttja/terasort.out
17/06/07 10:59:16 INFO mapreduce.Job:  map 100% reduce 95%
17/06/07 10:59:17 INFO mapreduce.Job:  map 100% reduce 97%
17/06/07 10:59:19 INFO mapreduce.Job:  map 100% reduce 98%
17/06/07 10:59:20 INFO mapreduce.Job:  map 100% reduce 99%
17/06/07 10:59:23 INFO mapreduce.Job:  map 100% reduce 100%
17/06/07 10:59:23 INFO mapreduce.Job: Job job_1496842591201_0006 completed successfully
17/06/07 10:59:23 INFO mapreduce.Job: Counters: 50
        File System Counters
                FILE: Number of bytes read=4443106801
                FILE: Number of bytes written=8823905319
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=10000046190
                HDFS: Number of bytes written=10000000000
                HDFS: Number of read operations=924
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=20
        Job Counters
                Launched map tasks=298
                Launched reduce tasks=10
                Data-local map tasks=297
                Rack-local map tasks=1
                Total time spent by all maps in occupied slots (ms)=2834317
                Total time spent by all reduces in occupied slots (ms)=759580
                Total time spent by all map tasks (ms)=2834317
                Total time spent by all reduce tasks (ms)=759580
                Total vcore-seconds taken by all map tasks=2834317
                Total vcore-seconds taken by all reduce tasks=759580
                Total megabyte-seconds taken by all map tasks=2902340608
                Total megabyte-seconds taken by all reduce tasks=777809920
        Map-Reduce Framework
                Map input records=100000000
                Map output records=100000000
                Map output bytes=10200000000
                Map output materialized bytes=4342696148
                Input split bytes=46190
                Combine input records=0
                Combine output records=0
                Reduce input groups=100000000
                Reduce shuffle bytes=4342696148
                Reduce input records=100000000
                Reduce output records=100000000
                Spilled Records=200000000
                Shuffled Maps =2980
                Failed Shuffles=0
                Merged Map outputs=2980
                GC time elapsed (ms)=43810
                CPU time spent (ms)=1487130
                Physical memory (bytes) snapshot=150567321600
                Virtual memory (bytes) snapshot=485899706368
                Total committed heap usage (bytes)=173733314560
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters
                Bytes Read=10000000000
        File Output Format Counters
                Bytes Written=10000000000
17/06/07 10:59:23 INFO terasort.TeraSort: done

real    4m38.872s
user    0m8.785s
sys     0m0.409s

