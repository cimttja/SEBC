Fastest

	teragen

		mapreduce.job.maps=8
		Reducer containers=4
		mapreduce.map.memory.mb=512
		mapreduce.map.java.opts.max.heap=409

		real    1m1.602s
		user    0m5.701s
		sys     0m0.289s

	terasort

		mapreduce.job.maps=2
		Reducer containers=4
		mapreduce.map.memory.mb=512
		mapreduce.map.java.opts.max.heap=409

		real    1m28.070s
		user    0m8.143s
		sys     0m0.309s
		
Slowest

	teragen

		mapreduce.job.maps=2
		Reducer containers=4
		mapreduce.map.memory.mb=1024
		mapreduce.map.java.opts.max.heap=819

		real    1m20.515s
		user    0m6.322s
		sys     0m0.291s
	
	terasort
	
		mapreduce.job.maps=2
		Reducer containers=1
		mapreduce.map.memory.mb=512
		mapreduce.map.java.opts.max.heap=409

		real    2m31.193s
		user    0m7.961s
		sys     0m0.292s
		
		
All Logs:
Testing loop started on Thu Jun 8 07:12:28 EDT 2017
mkdir -p /user/cimttja/results
--------------------------------------------------
mapreduce.job.maps=2
Reducer containers=1
mapreduce.map.memory.mb=512
mapreduce.map.java.opts.max.heap=409

real    1m17.464s
user    0m5.659s
sys     0m0.291s

real    2m31.193s
user    0m7.961s
sys     0m0.292s
Deleted /user/cimttja/results/tg-10GB-2-1-512
Deleted /user/cimttja/results/ts-10GB-2-1-512
--------------------------------------------------
mapreduce.job.maps=2
Reducer containers=1
mapreduce.map.memory.mb=1024
mapreduce.map.java.opts.max.heap=819

real    1m18.682s
user    0m5.723s
sys     0m0.279s

real    2m11.702s
user    0m8.223s
sys     0m0.328s
Deleted /user/cimttja/results/tg-10GB-2-1-1024
Deleted /user/cimttja/results/ts-10GB-2-1-1024
--------------------------------------------------
mapreduce.job.maps=2
Reducer containers=4
mapreduce.map.memory.mb=512
mapreduce.map.java.opts.max.heap=409

real    1m17.383s
user    0m5.984s
sys     0m0.293s

real    1m28.070s
user    0m8.143s
sys     0m0.309s
Deleted /user/cimttja/results/tg-10GB-2-4-512
Deleted /user/cimttja/results/ts-10GB-2-4-512
--------------------------------------------------
mapreduce.job.maps=2
Reducer containers=4
mapreduce.map.memory.mb=1024
mapreduce.map.java.opts.max.heap=819

real    1m20.515s
user    0m6.322s
sys     0m0.291s

real    1m30.188s
user    0m7.653s
sys     0m0.331s
Deleted /user/cimttja/results/tg-10GB-2-4-1024
Deleted /user/cimttja/results/ts-10GB-2-4-1024
--------------------------------------------------
mapreduce.job.maps=8
Reducer containers=1
mapreduce.map.memory.mb=512
mapreduce.map.java.opts.max.heap=409

real    1m3.548s
user    0m5.799s
sys     0m0.280s

real    2m10.731s
user    0m7.866s
sys     0m0.319s
Deleted /user/cimttja/results/tg-10GB-8-1-512
Deleted /user/cimttja/results/ts-10GB-8-1-512
--------------------------------------------------
mapreduce.job.maps=8
Reducer containers=1
mapreduce.map.memory.mb=1024
mapreduce.map.java.opts.max.heap=819

real    1m4.575s
user    0m5.726s
sys     0m0.282s

real    2m12.660s
user    0m7.733s
sys     0m0.327s
Deleted /user/cimttja/results/tg-10GB-8-1-1024
Deleted /user/cimttja/results/ts-10GB-8-1-1024
--------------------------------------------------
mapreduce.job.maps=8
Reducer containers=4
mapreduce.map.memory.mb=512
mapreduce.map.java.opts.max.heap=409

real    1m1.602s
user    0m5.701s
sys     0m0.289s

real    1m38.364s
user    0m7.449s
sys     0m0.325s
Deleted /user/cimttja/results/tg-10GB-8-4-512
Deleted /user/cimttja/results/ts-10GB-8-4-512
--------------------------------------------------
mapreduce.job.maps=8
Reducer containers=4
mapreduce.map.memory.mb=1024
mapreduce.map.java.opts.max.heap=819

real    1m12.733s
user    0m5.955s
sys     0m0.304s

real    1m56.029s
user    0m7.960s
sys     0m0.364s
Deleted /user/cimttja/results/tg-10GB-8-4-1024
Deleted /user/cimttja/results/ts-10GB-8-4-1024
--------------------------------------------------
Testing loop ended on Thu Jun 8 07:38:26 EDT 2017
