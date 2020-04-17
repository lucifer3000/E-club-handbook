## Flip Flops

The basic difference between a latch and a flip flop is that laches are level triggered while flip flops are edge triggered.
There is a clock pulse attached with the flip flop and the flip flop works on the rising and falling edge of the clock.

<p align ="center">
<img src ="https://cs.nyu.edu/courses/fall01/V22.0436-001/lectures/figs/clock.png">
</p>

A clock is necessary because otherwise the inputs can change on their own and the storage of the previous output would not be made of much use.

Having understood the latches, flip flops are really easy to understand. Let's first go with the SR flip flop.

### SR Flip flop:

<p align ="center">
<img src = "https://www.gatevidyalay.com/wp-content/uploads/2018/06/Logic-Circuit-For-SR-Flip-Flop-Constructed-Using-NAND-Latch.png" height="400" width="400">
</p>

If the clock pulse is 0 above then the next part of the flip flop which is simply a NAND SR Latch cooresponds to the memory state as both inputs would be 1 to the latch.

If the clock pulse is 1 then S correspnds to (S.clk(1))' = S' and R = R' and the truth table is:

| Clk | S | R |    Q   |   Q'   |                                                
|:---:|---|---|:------:|:------:|
|     |   |   |        |        |
|  0  | x | x | Memory | Memory |
|  1  | 0 | 0 | Memory | Memory |           
|  1  | 0 | 1 |    0   |    1   |            
|  1  | 1 | 0 |    1   |    0   |
|  1  | 1 | 1 |    -   |    -   |

**OR**

| Clk | S | R | Q(n+1) |
|:---:|:-:|:-:|:------:|
|  0  | x | x |  Q(n)  |
|  1  | 0 | 0 |  Q(n)  |
|  1  | 0 | 1 |    0   |
|  1  | 1 | 0 |    1   |
|  1  | 1 | 1 |    -   |

Here if S = 0 and R = 0 it would provide the SR latch with 1 and 1 hence the memory state.Similarly for others. If we look at the last case it would provide the SR Latch with 0 and 0 hence the forbidden condition which is an anomaly of the SR flip flop and this leads to the JK Flip Flop.

The characteristic table is:

| Q(n) | S | R | Q(n+1) |
|:----:|:-:|:-:|:------:|
|   0  | 0 | 0 |    0   |
|   0  | 0 | 1 |    0   |
|   0  | 1 | 0 |    1   |
|   0  | 1 | 1 |    -   |
|   1  | 0 | 0 |    1   |
|   1  | 0 | 1 |    0   |                
|   1  | 1 | 0 |    1   |
|   1  | 1 | 1 |    -   |

You don't need to memorize this , just by looking at the truth table you can make the characteristic tableby lokking at the values of S,R,Q(n) to find the value of Q(n+1) like for S = 0, R = 0, Q(n) = 0 => Q(n+1) = Q(n) = 0.

There is also one excitation table in which we have the outputs(Q(n) & Q(n+1)) with us and we need to compute the inputs (S,R) with it.

| Q(n) | Q(n+1) | S | R |
|:----:|:------:|:-:|:-:|
|   0  |    0   | 0 | x |
|   0  |    1   | 1 | 0 |
|   1  |    0   | 0 | 1 |
|   1  |    1   | x | 0 |             **x = don't care (can be 0 or 1)**


## J K Flip Flop:

Due to the shortcoming of the SR flip flop, JK flip flop in which for every set of input there is an output. It is completely similar to the SR flip flop just having an output value for the forbidden states also.

<p align = "center">
<img src = "https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2017/01/JK_flip.png" width="500" >
</p>

The truth table shown above have just the order of inputs different. You can easily understand it by referring below.

#### Working:

The outputs Q and Q' are fed back as inputs which make the difference. Now when clk=J=K=1 and let's say Q =0 and Q'=1. Now e=when Q is fed to the NAND2 it would result 1, and when Q' fed to NAND1 it would result 0. Thus comparing with the part2 which is the NAND latch it would result Q=1 and Q'=0.

Now when it is again given as feedback, this would result 1 from NAND1 and 0 from NAND2 thus changing the outputs Q=0 and Q'=1. So it feels as if it results in Q(n)' on every run.

| Clk | S | R | Q(n+1) |
|:---:|:-:|:-:|:------:|
|  0  | x | x |  Q(n)  |
|  1  | 0 | 0 |  Q(n)  |
|  1  | 0 | 1 |    0   |
|  1  | 1 | 0 |    1   |
|  1  | 1 | 1 |  Q(n)'   |     ----> This Q(n)' is known as **Toggling**  


#### The Race Around Problem

If J=K=1, and if clk=1 for a long period of time, then Q output will toggle as long as CLK is high, which makes the output of the flip-flop unstable or uncertain. This problem is called race around condition in J-K flip-flop.

<p align="center">
<img src = "https://3.bp.blogspot.com/-0hCoTTkoe58/UvOL-5QLo_I/AAAAAAAAANE/M1o4vVKoHhE/s1600/untitled.png" height="200">
</p>

This problem (Race Around Condition) can be avoided by ensuring that the clock input is at logic “1” only for a very short time. This introduced the concept of **Master Slave JK flip flop**.

#### Master Slave Condition



