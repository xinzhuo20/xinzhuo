Problem (a)
Let Pulg,0) and Pig,0) be the respective probabilities that Magnus wins the championship when he requires i points to score from the remaining g games, while currently playing as white (black).
Suppose, there are g games left and currently, he is playing as white.
If he wins (with probability w_w), then he needs i-1 points to score from the remaining g-1 games, while currently playing as black. The probability is Pilg-1,1-1)
If he draws (with probability w_d), then he needs \left (i-\frac{1}{2} \right ) points to score from the remaining g-1 games, while currently playing as black. The probability is P_b\left ( g-1, i-\frac{1}{2} \right )
If he loses (with probability w_l), then he still needs i points to score from the remaining g-1 games, while currently playing as black. The probability is P_b(g-1, i)
So, we have the following recurrence:
P_w(g, i) = w_wP_b(g - 1, i-1) + w_dP_b\left ( g - 1, i - \frac{1}{2} \right ) + w_lP_b(g - 1, i)
Following a similar agument, we have another recurrence if he is currently playing as black:
Polg, i) = bwPulg – 1,– 1) + bxPw (9-1, i – + b1 Pu(9 – 1, 1)
So, what are the base cases?
If g=0, then P_w(0,i)=P_b(0,i)=\begin{cases} 1 \text{ if } i= 0\\ 0 \text{ otherwise}\\ \end{cases}
If i=0, then P_w(g,0)=P_b(g,0)=1 . Winning is guaranteed since he does not need to score any point.
If i = 0,5, then
\begin{align*} &P_w(g, 0.5) = w_w + w_d + w_lP_b(g - 1, 0.5)\\ &P_b(g, 0.5) = b_w + b_d + b_lP_w(g - 1, 0.5)\\ &P_w(1, 0.5)=w_w+w_d\\ &P_b(1, 0.5)=b_w+b_d \end{align*}
 
Problem (b)
To make a DP algorithm, we need to store two matrices, one for white and one for black.
What should be their sizes? They are (n+1)\times (2n+1)
The rows are for number of games left, 0,1,2,3,\dots,n
The columns are for half points, 0,1,2,3,\dots,2n . Here, k^{th} place means k/2 points.
To win, you need to score at least n/2 points in n games as tie is also a win.
def win(n):
W=[[0 for j in range(2n+1)]]*(n+1)
W=[[0 for j in range(2n+1)]]*(n+1)
W[0][0]=1
B[0][0]=1
for g in range(n+1):
W[g][0]=1
B[g][0]=1
for g in range(1,n+1):
W[g][1] = w_w + w_d + w_l*B[g-1][1]
B[g][1] = b_w + b_d + b_l*W[g-1][1]
for i in range(1,n+1):
W[g][2i] = w_w*B[g-1][2i-2] + w_d*B[g-1],[2i-1]+ w_l*B[g-1][2i]
B[g][2i] = b_w*W[g-1][2i-2] + b_d*W[g-1],[2i-1]+ b_l*W[g-1][2i]
return W[n][n]
