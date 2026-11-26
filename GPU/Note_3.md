In this section, why dose the GPU divide an entire task into several parts and how does it finish this procedure?
First, it is decided by threads. Each thread will deal with its task by GPU.
Second, when the process (threadIdx.x) is created, in this code, it is decided by the n(input).
Finally, the number of the thread are depended on the data.

<img width="785" height="817" alt="image.png" src="https://github.com/user-attachments/assets/debfe537-d2c4-4837-a750-b9384c467303" />
