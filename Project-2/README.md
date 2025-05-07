|Thread<br>Count|Wall Clock<br>Time|User Time|System Time|Speedup|
|:--:|--:|--:|--:|:--:|
|1|14.40|13.90| 0.41|1.00|
|2| 8.99|17.01| 0.51| 1.60|
|3| 5.55|15.01| 0.71| 2.59|
|4| 4.57|16.07| 0.77| 3.15|
|5| 3.80|16.10| 0.92| 3.79|
|6| 3.31|16.30| 1.04| 4.35|
|7| 2.93|16.35| 1.10| 4.91|
|8| 2.73|17.02| 1.21| 5.27|
|16| 1.94|18.18| 2.95| 7.42|
|24| 1.86|18.86| 7.50| 7.74|
|32| 1.80|18.62|14.00| 8.00|
|40| 1.81|17.98|22.75| 7.96|
|48| 1.81|17.17|30.59| 7.96|
|56| 1.85|16.97|36.46| 7.78|
|64| 1.83|16.61|41.89| 7.87|
|72| 1.87|17.21|28.71| 7.70|
|80| 1.86|17.01|35.90| 7.74|

<img width="448" alt="Image" src="https://github.com/user-attachments/assets/ef0dd38f-7caa-4b86-9e37-e43bf4193436" />

More threads aren't necessarily better because eventually the computer wont be able to use as many cores as desired. It was a limit on how many threads it can use, the number of cores it has, so after this amount is exceeded using more threads wont improve the speed. Its similar to the turnstiles at Disney World because each turnstile is essentially a core in the computer and once all of them are being used at the same time, that will be the max speed people can get through them at.  

I don't think it is possible to get perfect scaling. The computer will never be perfectly efficient in synchronizing parallel threads so there will always be a small delay which will add to the time.

$$ speedup = \frac{1}{1 - p + \frac{p}{16}} = 0.996$$

1 thread = 1 speedup
7 threads = 4.91 speedup
slope = (4.91-1) / (7-1) = 0.652 

This linear trend continues until about 16 threads, and after this is when it begins to flatten out. I think this is because we have 16 cores to work with and after that, the number of threads increasing does not increase how many cores are being used, so the rate of speedup drops off.
