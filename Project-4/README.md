
Part 1:
For the code, I essentially just rewrote the example from the slides but used the equation from the c++ reference in the assignment in place of the one from the slides. 

Timings that I got:
CPU:
|Vector<br>Length|Wall Clock<br>Time|User Time|System Time|
|:--:|--:|--:|--:|
|10| 0.00| 0.00| 0.00|
|100| 0.00| 0.00| 0.00|
|1000| 0.00| 0.00| 0.00|
|10000| 0.00| 0.00| 0.00|
|100000| 0.00| 0.00| 0.00|
|1000000| 0.00| 0.00| 0.00|
|5000000| 0.02| 0.00| 0.02|
|100000000| 0.53| 0.09| 0.43|
|500000000| 2.68| 0.43| 2.25|
|1000000000| 5.37| 0.80| 4.56|
|5000000000|34.88| 6.19|28.68|

GPU:
|Vector<br>Length|Wall Clock<br>Time|User Time|System Time|
|:--:|--:|--:|--:|
|10| 0.30| 0.05| 0.24|
|100| 0.28| 0.05| 0.23|
|1000| 0.28| 0.05| 0.22|
|10000| 0.28| 0.05| 0.22|
|100000| 0.28| 0.05| 0.23|
|1000000| 0.28| 0.05| 0.22|
|5000000| 0.30| 0.06| 0.23|
|100000000| 0.61| 0.13| 0.48|
|500000000| 1.82| 0.45| 1.36|
|1000000000| 3.31| 0.84| 2.46|
|5000000000|16.73| 4.02|12.70|

It seems that the CUDA does have a solid improvement on the runtime for large data size runs, but is actually worse for the small data sizes. It seems that there is more system time required when the CUDA version runs which doesn’t have much of an effect when the data size is large enough, but for the smaller ones that system time ends up greatly increasing the runtime relative to what it was.

Part 2:
For this code, I started with the contents of the nested for loop as the hint suggested, and from there used the block.Idx, blockDim, and threadIdx multiplied together as my values for x & y rather than the for loops. I compared these x and y values with width and height to know when to exit, and I changed how the Complex values were declared to make them work. I also changed the color a bit to make it more exciting.

.ppm file output:
<img width="1005" alt="Screenshot 2025-05-11 at 10 18 33 PM" src="https://github.com/user-attachments/assets/35b3d497-087f-42b8-bf6a-24fc6f464342" />
