
|Unoptimized:|Real|User|System|Memory (KB)|Throughput (KB/Sec)|Performance Improvement|
|:--:|--:|--:|--:|--:|--:|:--:|
|Hash00|360.80|344.04|8.62|2912|8.07|N/A|
|Hash01    |     18.05  |  16.52    |  1.40   |     2900       |         160.66     |               19.98x|
|Hash02     |    15.69 |   14.26    |  1.32    |    2888       |         184.06         |           22.99x|
|Hash03     |    16.41  |  15.17    |  1.12    |    2900         |       176.72        |            21.98x|
|Hash04     |    14.45   | 13.84   |   0.50   |    5012356     |       346,875.84    |              24.96x|



|Optimized (OPT="-O2"): |  Real  |  User  |  System  |  Memory (KB)  |  Throughput (KB/Sec)  |  Performance Improvement|
|:--:|--:|--:|--:|--:|--:|:--:|
|Hash00       |           343.02 |  331.26  |   7.59   |      2896       |         8.44         |            1.05x|
|Hash01       |             8.37   |  6.93    |  1.25     |    2880        |       344.08          |          43.10x|
|Hash02       |             8.19   |  6.89   |   1.18     |    2892         |      353.11            |        44.05x|
|Hash03       |             8.08  |   6.83   |   1.13     |    2896        |       358.41          |          44.65x|
|Hash04        |            7.42   |  6.66    |  0.57    |    5010640     |        675,288.41       |         48.62x|





What operation do you think accounts for most of hash-00's runtime?

I believe that the “input >>” operation accounts for most of hash-00's runtime. This operation seems to be an outlier whereas most other programs use “input.read” to gather data.




hash-01 and hash-02 both dynamically allocate memory for each hash computation. Is there much difference time-wise between their two allocation methods?

There seems to be a slight advantage to hash-02’s allocation method. In both the unoptimized and O2 optimized tests hash-02 is able to run more quickly than hash-01.




hash-03 avoids the allocation by using a fixed-size array.  Is there an appreciable speed difference?

There is not an appreciable speed difference from using this different method. In the unoptimized test it is actually slower than hash-02 by 0.72 seconds, and in the O2 optimized version it is only 0.11 seconds faster than hash-02.




Why is hash-04's memory usage so much larger than any of the other versions?  Hint: recall when we discussed how the operating system reads a file and makes it available to an application.  Specifically, the O/S will transfer data from disk to its own memory, and then copy from there into buffers provided by the application.  In the memory map case, the O/S is merely sharing the copy of the file's data that is in its (the O/S's) memory, and not making an additional copy from its memory into memory only in the application

hash-04's memory usage is so much larger because of the mmap function that is called. It maps the entire file in that one call which takes up a very large amount of space. In the other versions of the program they iterate through the data and take pieces as needed, but here it is all collected at once which is the cause of the large memory usage. 




What other compiler options did you try, and did they help at all?

The other compiler options that I tried were OPT="-O1” as well as OPT="-O2 -funroll-loops". When using O1, it was still faster than all of the unoptimized outputs, but surprisingly, it was also faster than O2 in the hash-01 and hash-02 programs. When using O2 -funroll-loops, it was also able to beat the normal O2 optimization in hash-02 and hash-04 programs. It seems that when using these optimizations, there may be different tasks that they work more efficiently on compared to other optimization types. 
