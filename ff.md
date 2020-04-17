## Flip Flops

The basic difference between a latch and a flip flop is that laches are level triggered while flip flops are edge triggered.
There is a clock pulse attached with the flip flop and the flip flop works on the rising and falling edge of the clock.

<p align ="center">
<img src ="https://cs.nyu.edu/courses/fall01/V22.0436-001/lectures/figs/clock.png">
</p>

A clock is necessary because otherwise the inputs can change on their own and the storage of the previous output would not be made of much use.

Having understood the latches, flip flops are really easy to understand. Let's first go with the SR flip flop.

### SR Flip Flop

<p align ="center">
<img src = "https://www.gatevidyalay.com/wp-content/uploads/2018/06/Logic-Circuit-For-SR-Flip-Flop-Constructed-Using-NAND-Latch.png" height="400" width="400">
</p>

If the clock pulse is 0 above then the next part of the flip flop which is simply a NAND SR Latch corresponds to the memory state as both inputs would be 1 to the latch.

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

You don't need to memorize this , just by looking at the truth table you can make the characteristic table by looking at the values of S,R,Q(n) to find the value of Q(n+1) like for S = 0, R = 0, Q(n) = 0 => Q(n+1) = Q(n) = 0.

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

The outputs Q and Q' are fed back as inputs which make the difference. Now when clk=J=K=1 and let's say Q =0 and Q'=1. Now when Q is fed to the NAND2 it would result 1, and when Q' is fed to NAND1 it would result 0. Thus comparing with the part2 which is the NAND latch it would result Q=1 and Q'=0.

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

<p align="center">
<img src = "https://media.geeksforgeeks.org/wp-content/uploads/flipflop-1.jpg" height="400">
</p>

The two blocks refer to the actual structure of the J K filp flop. In the master-slave condition another JK flip flop is added and the ouput of the second flip flop is feedbacked as input to the first flip flop + the same clock is attached with a NOT gate.

The problem of race around arises when clk=J=K=1 , so let's discuss that case.First see this:

<p align="center">
<img src ="https://media.geeksforgeeks.org/wp-content/uploads/flipflop-diag-1.jpg">
</p>  

When the clock starts , master FF functions and the slave FF acts as a memory state as the clock signal is zero due to NOT gate. Now when J=1 and K=1 and on the rising edge of the clock , the Q signal becomes high of master FF and it would remain high till the second rising edge. 

On the falling edge of the clock the slave FF becomes active and the master FF acts as a memory state, thus it would remain high as said above.Now output of first FF is fed to slave FF which produces the same output as master FF thus it remains high till the second falling edge.

That output is fed back to master FF and on the second rising edge(means slave FF acts as memory state now), toggling takes place and thus the sginal Q(m) becomes low. Now, at the second falling edge, again the input is given to slave FF and toggling takes place and the process repeats itself.

**This makes the Master-Slave J-K flip flop a Synchronous device as it only passes data with the timing of the clock signal**


### D Flip Flop

<p align="center">
<img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2017/01/D-logic-diag-300x123.png" height="200">
</p>  

<p align="center">
<img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2017/01/D-flip-flop.png" width="200" height="200">
</p>


### T Flip Flop

<p align="center">
<img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2017/01/T-logic-diag-300x143.png" height="200" width="300">
</p>  

<p align="center">
<img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2017/01/T-flip-flop-300x127.png" height="200" width="300">
</p>  
