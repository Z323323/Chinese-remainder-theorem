# Chinese-remainder-theorem
<p>The Chinese remainder theorem is one of the most useful and important foundation theorems regarding cryptography and modular arithmetic.<br>
$x \equiv a_{1}\mod m_{1}$ <br>
$\dots$ <br>
$x \equiv a_{n}\mod m_{n}$ <br>
has a unique solution for x modulo M where $M = m_{1}\dots m_{n}$ and $m_{1}\dots m_{n}$ are pairwise coprime. <br>
This is useful in reverse direction too, i.e. if a congruence works for a modulo which is a multipication of primes, then it will work for those primes individually. <br>
This whole work is home-made. I already posted this on my X account, here I'll try to correct every potential error and inconsistence and provide a complete proof.<br>
</p>

## Building the solution
<p>We take $N_{i}$ as the multiplication of every $m_{j}$ where 'j' means 'every $m_{i}$ with 'i' from 1 to 'n' except $m_{i}$'. I know this sounds completely no-sense. Example: $N_{1} = m_{2}m_{3}\dots$ or $N_{2} = m_{1}m_{3}\dots$. <br>
We know gcd($N_{i}$, $m_{i}$) = 1 because every $m_{i}$ is pairwise coprime. <br>
We use the Extended Euclidean Algorithm or another algorithm/formula to compute the mutiplicative inverse of every $N_{i}$ and we call it $n_{i}$. Recalling Bezout's Identity: <br>
$N_{i}n_{i} + (- z_{i})m_{i} = 1$ <br>
$N_{i}n_{i} - 1 = z_{i}m_{i}$ <br>
$N_{i}n_{i} \equiv 1\mod m_{i}$ <br>
This is not actually very important, just take the last congruence and proceed. The Bezout's Identity is useful to understand the Extended Euclidean Algorithm, but that's another problem, here we need to keep the focus on the CRT, furthermore the multiplicative inverse is computable using the Fermat's Little Theorem and the Montgomery optimization. Let's go over.<br>
To prove the theorem, we need to compute a solution for the system of congruences and prove the solution is unique having $m_{1}\dots m_{n}$ coprime pairwise.
We can provide one solution for every congruence (for the moment):
$x_{i} \equiv a_{i}N_{i}n_{i}\mod m_{i}$. <br>
This is quite obvious, we didn't do basically anything since $N_{i}n_{i} \equiv 1\mod m_{i}$. <br>
So why should we do something that is basically useless? This will be clear understanding the final solution of the system (it's not useless).
Now the actual problem is to solve this system for one $x$ not every $x_{i}$. <br>
Solution: $x \equiv \sum_{i = 1}^{n} a_{i}N_{i}n_{i}(\mod \prod_{i = 1}^{n} m_{i})$ <br>
This could look scary at first but we just summed every $x_{i}$ and computed the modulo by the product of every $m_{i}$. Now the real problem is to understand why this solution works, and why it's unique. <br>
To better understand this, let's restrict the reasoning to a couple of congruences instead of the formalization (which works for any number of congruences): <br>
$x \equiv a_{1}\mod m_{1}$ <br>
$x \equiv a_{2}\mod m_{2}$ <br>
Solution: $x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ <br>

## Proof of correctness and uniqueness

<p>Let's try to show this solution works for $x_{1} \equiv a_{1}\mod m_{1}$, then all other solutions will follow the same reasoning proving the solution is correct.<br>
$N_{1} = m_{2}$ (it would be $N_{1} = m_{2}m_{3}\dots$ in the 'general' case), this means that $N_{1}$ 'erase' $m_{2}$, i.e. $N_{1} \equiv 0\mod m_{2}$ (in the 'general' case it would 'erase' every $m_{j}$ but not $m_{i}$). <br>
This means that taken: <br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$, <br>
if we take into consideration $m_{2}$ we can say that this congruence is equivalent to: <br>
$x \equiv a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ <br>
and this one to: <br>
$x \equiv a_{2}N_{2}n_{2} (\mod m_{2})$ <br> following the same reasoning ($N_{2} = m_{1}$). The same goes for: <br>
$x \equiv a_{1}N_{1}n_{1} (\mod m_{1})$ <br>
At the same time $N_{1}n_{1} \equiv 1\mod m_{1}$ (we started from $N_{i}n_{i} \equiv 1\mod m_{i}$). <br> This leads to: $x \equiv a_{1} \mod m_{1}$. <br>
This proves correctness and uniqueness. Uniqueness is more subtle, note that 'uniqueness' doesn't mean this is the only solution which solve the system, but that this solution is is unique modulo $m_{1}\dots m_{n}$. Since it's not possible to restrict $M = m_{1}\dots m_{n}$ more than this and solve every congruence simultaneously, by construction the solution is unique modulo $m_{1}\dots m_{n}$ (this is also because $m_{1}\dots m_{n}$ are coprime pairwise). <br>
Then $x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ solves $x \equiv a_{1}\mod m_{1}$ and following the same reasoning: <br>
$x \equiv a_{2}\mod m_{2}$ (simultaneously). Generalizing for: <br>
$x \equiv \sum_{i = 1}^{n} a_{i}N_{i}n_{i}(\mod \prod_{i = 1}^{n} m_{i})$ this solves: <br>
$x \equiv a_{1}\mod m_{1}$ <br>
$\dots$ <br>
$x \equiv a_{n}\mod m_{n}$ <br>
simultaneously and uniquely.
</p>
