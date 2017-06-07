[root@ip-172-31-16-170 hadoop]# sudo -su cimttja hdfs dfs -mkdir /user/cimttja/preciouss
[root@ip-172-31-16-170 hadoop]# sudo -su cimttja hdfs dfs -put /home/cimttja/SEBC-master.zip /user/cimttja/precious
[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hdfs dfs -chown -R cimttja:supergroup /user/cimttja/
--> enable shnapshots in gui
[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hdfs dfs -rm -r -skipTrash /user/cimttja/precious
rm: The directory /user/cimttja/precious cannot be deleted since /user/cimttja/precious is snapshottable and already has snapshots
[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hdfs dfs -rm -r -skipTrash /user/cimttja/precious/SEBC-master.zip
Deleted /user/cimttja/precious/SEBC-master.zip
--> restore snapshots
[root@ip-172-31-16-170 hadoop]# sudo -su hdfs hdfs dfs -ls /user/cimttja/precious
Found 1 items
-rw-r--r--   3 hdfs supergroup     476522 2017-06-07 11:29 /user/cimttja/precious/SEBC-master.zip
[root@ip-172-31-16-170 hadoop]#