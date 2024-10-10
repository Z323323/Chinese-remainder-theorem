# Chinese-remainder-theorem
<p>The Chinese remainder theorem is one of the most useful and important foundation theorems regarding cryptography and modular arithmetic.<br>
$x \equiv a_{1}\mod m_{1}$ <br>
$\dots$ <br>
$x \equiv a_{n}\mod m_{n}$ <br>
has a unique solution for x modulo M where $M = m_{1}\dots m_{n}$ and $m_{1}\dots m_{n}$ are pairwise coprime. <br>
This is useful in reverse direction too, i.e. if a congruence works for a modulo which is a multipication of coprimes, then it will work for those coprimes individually. <br>
This whole work is home-made. I already posted this on my X account, here I'll try to correct every potential error and inconsistence and provide a complete proof.<br>
Note also that a lot of things come directly from https://crypto.stanford.edu/pbc/notes/numbertheory/crt.html even though are not copy-pasted but I tried to rielaborate in order to make them more complete and easy to digest.
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

## Example

<p>We could write for ex.: <br>
$17 \in Z_{35}$ as $(2, 3) \in Z_{5} * Z_{7}$<br>
or <br>
$1 \in Z_{pq}$ as $(1, 1) \in Z_{p} * Z_{q}$. <br>
To better clarify the first ex. which is not obvious, note that $N_{i}n_{i} \equiv 1\mod m_{i}$ doesn't mean that $N_{i}n_{i} = 1$: <br>
$x \equiv 2\mod 5$ <br>
$x \equiv 3\mod 7$ <br>
$\equiv$<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ <br>
-----<br>
$N_{1} = 7$<br>
$n_{1} =$ ? <br>
$7 * n_{1} + (- z_{1}) * 5 = 1$ <br>
$7 * 3 - 1 = 4 * 5$ --- here I applied Bezout's Identity by hand, in a real scenario EEA or another algorithm would be mandatory.<br>
$n_{1} = 3$<br>
$a_{1}N_{1}n_{1} = 2 * 7 * 3 = 42$<br>
-----<br>
$N_{2} = 5$ <br>
$n_{2} =$ ? <br>
$5 * n_{2} + (- z_{2}) * 7 = 1$ <br>
$5 * 3 - 1 = 2 * 7$ <br>
$n_{2} = 3$<br>
$a_{2}N_{2}n_{2} = 3 * 5 * 3 = 45$<br>
-----<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ <br>
-><br>
$x \equiv 42 + 45 (\mod 35)$ <br>
-><br>
$x \equiv 87 \mod 35$ <br>
-><br>
$x \equiv 17 \mod 35$ <br>
-----<br>
$x \equiv 2\mod 5$ <br>
$x \equiv 3\mod 7$ <br>
$\equiv$<br>
$x \equiv 17 \mod 35$ <br>
</p>

## Further implications and usage of this theorem
<p>This theorem is more powerful than what it looks.<br>
Suppose we have a couple numbers $x, y \in Z_{pq}$ and that these numbers correspond to $(a, b), (c, d) \in Z_{p} * Z_{q}$. <br>
From the example above is clear that $Z_{p}$ and $Z_{q}$ are both already composed of 2 elements of two other $Z_{?}$, this means that $Z_{pq}$ has a modulo of 4 coprimes multiplied. <br>
The interesting (and powerful) thing which is not clear at a first sight is that doing $x + y$ is the same as doing $(a + c, b + d)$ and doing $xy$ is the same as $(ac, bd)$. This means that for ex. if we need to compute a power in $Z_{pq}$, we can use $Z_{p}$ and $Z_{q}$ instead, which is convenient: $17^{2} \mod 35$ is computable applying the CRT to $(2^{2}, 3^{2}) \in Z_{5} * Z_{7}$.<br>
Going back to $x + y$ and $xy$ reasoning, it's important to fully understand this behaviour. $(a, b), (c, d) \in Z_{p} * Z_{q}$ are numbers which are pairwise coprime (a, b, c, d are coprime), this example is slightly different from the example above, infact $Z_{p}$ and $Z_{q}$ represented like so are equivalent to $Z_{1_{?}} \dots Z_{4_{?}}$ since elements are not 'merged' but are 'paired'. This 'pairing' is a little bit misleading since the CRT doesn't care about order of 'subgroups'. Also, $Z_{pq}$ elements are not merged completely, otherwise its elements would be composed by 1 number and not 2 (x, y). The 'merge' is only considered for $Z_{1_{?}}$, $Z_{3_{?}}$ -> $x$ and $Z_{2_{?}}$, $Z_{4_{?}}$ -> $y$. And this is why $x + y$ is the same as doing $(a + c, b + d)$ and doing $xy$ is the same as $(ac, bd)$. <br>
Another important thing is to fully comprehend how the CRT 'map' two 'subrgroups' modulo coprimes to a 'super-group' in order to make operations (+, -, *, /) hold. Here to avoid putting a bunch of formal useless stuff just note that since these: <br>
$x \equiv a_{1}\mod m_{1}$ <br>
$\dots$ <br>
$x \equiv a_{n}\mod m_{n}$ <br>
are fully 'mapped' into this: <br>
$x \equiv \sum_{i = 1}^{n} a_{i}N_{i}n_{i}(\mod \prod_{i = 1}^{n} m_{i})$ <br>
then these (and every other operation performed $\mod m_{1}\dots m_{n}$): <br>
$x \equiv a_{1} + z_{1}\mod m_{1}$ <br>
$\dots$ <br>
$x \equiv a_{n} + z_{n}\mod m_{n}$ <br>
will be fully 'mapped' into: <br>
$x \equiv \sum_{i = 1}^{n} (a_{i} + z_{i})N_{i}n_{i}(\mod \prod_{i = 1}^{n} m_{i})$ <br>
<br>
The last thing to notice about this whole theorem is that the restriction imposed by it doesn't concern primes but co-primes, and since the powers of primes are co-prime pairwise this means that we can use powers of primes as 'sub-groups' to prove statements on 'super-groups' which identify all integer numbers: <br>
$integer = p_{1}^{k_{1}} \dots p_{n}^{k_{n}}$ <br>
-CRT-> <br>
$Z_{integer} = Z_{p_{1}^{k_{1}}} \dots Z_{p_{n}^{k_{n}}}$
</p>
