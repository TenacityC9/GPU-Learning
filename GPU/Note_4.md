In this section, I have learned grouping the threads.
First of all, every thread has only two roles: its location and sequence in its belonging group. If the number of thread is smaller than the task, it will only complete the former ones(number), or called repeating. Others are not done.
Therefore, it is bright ways to tell the threads where it is. In a word, make its index equal to blockIdx.x * blockDim.x + threadIdx.x.

```cpp
__global__ void add(float* a, float* b, float* c, int n) {
    int i = blockIdx.x * blockDim.x + threadIdx.x;
    c[i] = a[i] + b[i];
}
```


However, what will the other threads happen to do? From programming course, we have known the ”Array out of bounds“. It will report the error by complier, but the computer doesn't know it is out of the bound. Thus, it will impact other data.
Interesting, so we add the check to find whether the unit is out of the bound.
```cpp
__global__ void add(float* a, float* b, float* c, int n) {
    int i = blockIdx.x * blockDim.x + threadIdx.x;
    if (i < n) {
        c[i] = a[i] + b[i];
    }
}
// 启动：派 3 组，每组 4 个线程
add<<<3, 4>>>(d_a, d_b, d_c, n)
```
Other threads will be out of bound unless it has boundary check.

<img width="2033" height="607" alt="7e33661f0df2dfd832c90afd2ef7c3c8" src="https://github.com/user-attachments/assets/97036a81-747e-44c4-86c7-34d9b83f51f8" />


>[!NOTE]
>The theory of it:
>
>1.block (blockIdx.x * blockDim.x)
>
>2.grid (gridDim.x)
>
>3.global index (blockIdx.x * blockDim.x + threadIdx.x)
