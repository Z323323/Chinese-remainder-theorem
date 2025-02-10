# Chinese remainder theorem

<p>
  
The Chinese remainder theorem is one of the most useful and important foundation theorems regarding cryptography and modular arithmetic.
  
$x_{1} \equiv a_{1} \mod m_{1}$ <br>
$\dots$ <br>
$x_{n} \equiv a_{n} \mod m_{n}$

has a unique solution $x \mod M$ where $M = m_{1} \dots m_{n}$ and $m_{1} \dots m_{n}$ are pairwise coprime.

This is useful in reverse direction too, that is, if a congruence works for a modulo which is a multiplication of coprimes, then it will work for those coprimes individually.

</p>

## Building the solution
<p>
  
  We take $N_{i}$ as the multiplication of every $m_{j}$ where $j$ means 'every $m_{i}$ with $i$ from $1$ to $n$ except $m_{i}$'. I know this sounds completely no-sense. 
  
  #### Example
  
  $N_{1} = m_{2}m_{3}\dots$
  
  or 
  
  $N_{2} = m_{1}m_{3}\dots$
  
We know $gcd(N_{i}, m_{i}) = 1$ because every $m_{i}$ is pairwise coprime. We use the Extended Euclidean Algorithm or another algorithm/formula to compute the mutiplicative inverse of every $N_{i}$ and we call it $n_{i}$. Recalling Bezout's Identity
  
$N_{i}n_{i} + (- z_{i})m_{i} = 1$<br>
$->$<br>
$N_{i}n_{i} - 1 = z_{i}m_{i}$<br>
$->$<br>
$N_{i}n_{i} \equiv 1 \mod m_{i}$

To prove the theorem, we need to compute a solution for the system of congruences and prove the solution is unique having $m_{1}\dots m_{n}$ coprime pairwise. We can see

$x_{i} \equiv a_{i}N_{i}n_{i}\mod m_{i}$

is a trivial but general solution for every congruence. This is quite obvious, we didn't do basically anything since $N_{i}n_{i} \equiv 1 \mod m_{i}$. So why should we do something that is basically useless? This will be clear understanding the final solution of the system (it's not useless). Now the actual problem is to solve this system for one $x$ not every $x_{i}$ and the final solution will be

$x \equiv \sum_{i = 1}^{n} a_{i}N_{i}n_{i} \mod \prod_{i = 1}^{n} m_{i}$

This could look scary at first but we just summed every $a_{i}$ and computed the modulo by the product of every $m_{i}$. Now the real problem is to understand why this solution works, and why it's unique. To better understand this, let's restrict the reasoning to a couple of congruences instead of the formalization (which works for any number of congruences).

$x_{1} \equiv a_{1} \mod m_{1}$<br>
$x_{2} \equiv a_{2} \mod m_{2}$<br>
$->$<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} \mod m_{1}m_{2}$

## Proof of correctness and uniqueness

<p>
  
  Let's see why the previous solution works for $x_{1} \equiv a_{1} \mod m_{1}$, then all other solutions will follow the same reasoning proving the solution is correct. We have
  
$N_{1} = m_{2}$ 

(it would be $N_{1} = m_{2}m_{3} \dots$ in the 'general' case), this means that $m_{2}$ 'erase' $N_{1}$, that is, $N_{1} \equiv 0 \mod m_{2}$ (in the 'general' case it would 'erase' every $N_{i}$ but not $N_{2}$). This means that taken
  
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} \mod m_{1}m_{2}$
  
if we take into consideration $m_{2}$ we can see that this congruence is equivalent to

$x \equiv a_{2}N_{2}n_{2} \mod m_{2}$<br>
$->$<br>
$x \equiv a_{2} \mod m_{2}$

and the same goes for

$x \equiv a_{1}N_{1}n_{1} \mod m_{1}$<br>
$->$<br>
$x \equiv a_{1} \mod m_{1}$

(etc. if we consider the general case) proving correctness and uniqueness. Uniqueness is more subtle, note that 'uniqueness' doesn't mean this is the only solution which solve the system, but that this solution is is unique modulo $m_{1} \dots m_{n}$. Since it's not possible to restrict $M = m_{1} \dots m_{n}$ more than this and solve every congruence simultaneously, by construction the solution is unique modulo $m_{1}\dots m_{n}$. Then

$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} \mod m_{1}m_{2}$ 

solves 

$x \equiv a_{1} \mod m_{1}$

and

$x \equiv a_{2}\mod m_{2}$ 

simultaneously and uniquely. Generalizing for

$x \equiv \sum_{i = 1}^{n} a_{i}N_{i}n_{i} \mod \prod_{i = 1}^{n} m_{i}$

this solves

$x \equiv a_{1} \mod m_{1}$<br>
$\dots$<br>
$x \equiv a_{n} \mod m_{n}$

simultaneously and uniquely.

</p>

## Example

<p>
  
  We could write for ex.

$17 \in Z_{35}$ as $(2, 3) \in Z_{5}Z_{7}$<br>
$or$<br>
$1 \in Z_{pq}$ as $(1, 1) \in Z_{p}Z_{q}$

To better clarify the first ex. which is not obvious let's delve it. (Also note that $N_{i}n_{i} \equiv 1 \mod m_{i}$ doesn't mean that $N_{i}n_{i} = 1$)

$x \equiv 2 \mod 5$<br>
$x \equiv 3 \mod 7$<br>
$\equiv$<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} \mod m_{1}m_{2})$

$-----$<br>
$N_{1} = 7$<br>
$n_{1} = ?$<br>
$7 \cdot n_{1} + (- z_{1}) \cdot 5 = 1$<br>
$7 \cdot 3 - 1 = 4 \cdot 5$ --- here I applied Bezout's Identity by hand, in a real scenario EEA or another algorithm would be mandatory.<br>
$n_{1} = 3$<br>
$a_{1}N_{1}n_{1} = 2 \cdot 7 \cdot 3 = 42$<br>
$-----$<br>
$N_{2} = 5$<br>
$n_{2} = ?$<br>
$5 \cdot n_{2} + (- z_{2}) \cdot 7 = 1$<br>
$5 \cdot 3 - 1 = 2 \cdot 7$<br>
$n_{2} = 3$<br>
$a_{2}N_{2}n_{2} = 3 \cdot 5 \cdot 3 = 45$<br>
$-----$<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} \mod m_{1}m_{2}$<br>
$->$<br>
$x \equiv 42 + 45 (\mod 35)$<br>
$->$<br>
$x \equiv 87 \mod 35$<br>
$->$<br>
$x \equiv 17 \mod 35$<br>
$-----$<br>
$x \equiv 2\mod 5$<br>
$x \equiv 3\mod 7$<br>
$\equiv$<br>
$x \equiv 17 \mod 35$<br>
$->$<br>
$17 \equiv 2\mod 5$<br>
$17 \equiv 3\mod 7$<br>

</p>

## Further implications and usage of this theorem
<p>This theorem is more powerful than what it looks.<br>
Suppose we have a couple numbers $x, y \in Z_{pq}$ and that these numbers correspond to $(a, b), (c, d) \in Z_{p} * Z_{q}$. <br>
The interesting (and powerful) thing which is not clear at a first sight is that doing $x + y$ is the same as doing $(a + c, b + d)$ and doing $xy$ is the same as $(ac, bd)$. This means that for ex. if we need to compute a power in $Z_{pq}$, we can use $Z_{p}$ and $Z_{q}$ instead, which is convenient: $17^{2} \mod 35$ is computable applying the CRT to $(2^{2}, 3^{2}) \in Z_{5} * Z_{7}$ (clearly convenient).<br>
Going back to $x + y$ and $xy$ examples, these are slightly different from the example above, indeed $Z_{p}$ and $Z_{q}$ represented like so are equivalent to $Z_{?_{1}} \dots Z_{?_{4}}$ since elements are not 'merged' but are 'paired'. This 'pairing' is a little bit misleading since the CRT doesn't care about order of 'subgroups'. Also, $Z_{pq}$ elements are not merged completely, otherwise its elements would be composed by $1$ number and not $2$ $(x, y)$. The 'merge' is only considered for $Z_{?_{1}}$, $Z_{?_{3}}$ -> $x$ and $Z_{?_{2}}$, $Z_{?_{4}}$ -> $y$. And this is why $x + y$ is the same as doing $(a + c, b + d)$ and doing $xy$ is the same as $(ac, bd)$.
Another important thing is to fully comprehend how the CRT 'map' two 'subrgroups' modulo coprimes to a 'super-group' in order to make operations $(+, -, *, /)$ hold. Here to avoid putting a bunch of formal (and therefore work :'D) stuff just note that since these:
  
$x \equiv a_{1}\mod m_{1}$ <br>
$\dots$ <br>
$x \equiv a_{n}\mod m_{n}$

are fully 'mapped' into this

$x \equiv \sum_{i = 1}^{n} a_{i}N_{i}n_{i}(\mod \prod_{i = 1}^{n} m_{i})$

then these (and every other operation performed $\mod m_{1}\dots m_{n}$)

$x \equiv a_{1} + z_{1}\mod m_{1}$ <br>
$\dots$ <br>
$x \equiv a_{n} + z_{n}\mod m_{n}$

will be fully 'mapped' into

$x \equiv \sum_{i = 1}^{n} (a_{i} + z_{i})N_{i}n_{i}(\mod \prod_{i = 1}^{n} m_{i})$

Here it's ¿clear? that any operation performed (must be repeated consistently for every $a_{i}$) will be reflected in the solution congruence. The summation performed into the solution formula and multiplication by $N_{i}n_{i}$ is quite misleading and magical. To better understand how this is possible, let's look again at the example above: $17^{2} \mod 35$. The biggest problem with operations made modulo $n$ is that are absolutely not intuitive, the modulo breaks our understanding of how things work, so to understand how this example works in both directions:

$(\sum_{i = 1}^{n} a_{i}N_{i}n_{i})^{2}(\mod \prod_{i = 1}^{n} m_{i})$<br>
$\equiv$<br>
$(\sum_{i = 1}^{n} a_{i}N_{i}n_{i})(\sum_{i = 1}^{n} a_{i}N_{i}n_{i})(\mod \prod_{i = 1}^{n} m_{i})$<br>
$\equiv$<br>
$(a_{i}N_{i}n_{i})^{2}(\mod \prod_{i = 1}^{n} m_{i})$<br>
$\equiv$<br>
$(a_{i})^{2}(\mod m_{i})$

The real proof of equivalence under every operation should include other cases.
<br>
The last thing to notice about this whole theorem is that the restriction imposed by it doesn't concern primes but co-primes, and since the powers of primes are co-prime pairwise this means that we can use powers of primes as 'sub-groups' to prove statements on 'super-groups' which identify all integer numbers:

$integer = p_{1}^{k_{1}} \dots p_{n}^{k_{n}}$ <br>
-CRT-> <br>
$Z_{integer} = Z_{p_{1}^{k_{1}}} \dots Z_{p_{n}^{k_{n}}}$
</p>

## Extending the reasoning to polynomials
<p>Example: we need to solve $x^{2} - 1  \mod 77 = 0$, or (rewritten):
  
$x^{2} \equiv 1 \mod 77$

Note that finding the solutions to this congruence means finding the roots of the 2nd degree polynomial and/or at the same time finding the square roots of $1 \mod 77$, hence it's a good example.
The first solution one could immediately think of is: $x = 1$ or $x = - 1$.<br>
It turns out that this is partially correct, i.e. is not the complete solution. From the CRT we know that:

$x^{2} - 1  \mod 77 = 0$ <br>
$\equiv$<br>
$x^{2} - 1  \mod 7 = 0$ <br>
$x^{2} - 1  \mod 11 = 0$

Now, since every congruence will have $2$ distinct solutions which depend on the degree of the poly (at most there will be $degree$ roots), and these solutions must be completely 'mapped' into $x^{2} - 1  \mod 77 = 0$, we will need to have a number of final solutions which is the product of the solutions of the single congruences.<br>
Let's solve this simple exercise noting that is basically the same as the previous example showed above: <br>

for $x^{2} - 1  \mod 7 = 0$ we will have $x = 1 \mod 7$ or $x = - 1 \mod 7$<br>
and,<br>
for $x^{2} - 1  \mod 11 = 0$ we will have $x = 1 \mod 11$ or $x = - 1 \mod 11$.<br>

Our solution ($x^{2} - 1  \mod 77 = 0$) will need to 'map' every different 'combination' of solutions of our starting congruences because every single 'sub-congruences' solutions case must covered, i.e. following the example we will actually need to cover these solutions:

$x \equiv 1  \mod 7$ <br>
$x \equiv 6  \mod 7$ <br>
$x \equiv 1  \mod 11$ <br>
$x \equiv 10  \mod 11$

And since our final solution will need to cover every case: <br>

1st solution&ensp;--- $x \equiv 1  \mod 7$ && $x \equiv 1  \mod 11$ <br>
2nd solution --- $x \equiv 1  \mod 7$ && $x \equiv 10  \mod 11$ <br>
3rd solution&ensp;--- $x \equiv 6  \mod 7$ && $x \equiv 1  \mod 11$ <br>
4th solution&ensp;--- $x \equiv 6  \mod 7$ && $x \equiv 10  \mod 11$ <br>
  
At first this looks strange because we set our mind to always have one single solution for a system of congruences, but remember that when a polynomial has more than one solution it means that our resulting CRT-congruence will have more than one solution too, following the rule of the product. <br>
Now since we know that in this case we will have 4 different solutions, we will apply the CRT 4 times to every 'combination' of 'sub-congruences' solutions.<br>

1st solution:<br>
$x \equiv 1  \mod 7$ <br> 
$x \equiv 1  \mod 11$ <br>
$\equiv$<br>
$x \equiv ?  \mod 77$ <br>
-----<br>
$N_{1} = 11$<br>
$n_{1} =$ ? <br>
$11 * n_{1} + (- z_{1}) * 7 = 1$ <br>
$11 * 2 - 1 = 3 * 7$ --- BI.<br>
$n_{1} = 2$<br>
$a_{1}N_{1}n_{1} = 1 * 11 * 2 = 22$<br>
-----<br>
$N_{2} = 7$ <br>
$n_{2} =$ ? <br>
$7 * n_{2} + (- z_{2}) * 11 = 1$ <br>
$7 * 8 - 1 = 5 * 11$ <br>
$n_{2} = 8$<br>
$a_{2}N_{2}n_{2} = 1 * 7 * 8 = 56$<br>
-----<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ <br>
-><br>
$x \equiv 22 + 56 (\mod 77)$ <br>
-><br>
$x \equiv 1 (\mod 77)$ <br>
This was quite obvious, but it's always better to verify. <br>
----------<br>

2nd solution: <br>
$x \equiv 1  \mod 7$ <br> 
$x \equiv 10  \mod 11$ <br>
$\equiv$<br>
$x \equiv ?  \mod 77$ <br>
-----<br>
$N_{1} = 11$<br>
$n_{1} =$ ? <br>
$11 * n_{1} + (- z_{1}) * 7 = 1$ <br>
$11 * 2 - 1 = 3 * 7$ --- BI.<br>
$n_{1} = 2$<br>
$a_{1}N_{1}n_{1} = 1 * 11 * 2 = 22$<br>
-----<br>
$N_{2} = 7$ <br>
$n_{2} =$ ? <br>
$7 * n_{2} + (- z_{2}) * 11 = 1$ <br>
$7 * 8 - 1 = 5 * 11$ <br>
$n_{2} = 8$<br>
$a_{2}N_{2}n_{2} = 10 * 7 * 8 = 56$<br>
-----<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ <br>
-><br>
$x \equiv 22 + 560 (\mod 77)$ <br>
-><br>
$x \equiv 43 (\mod 77)$ <br>
----------<br>

3rd solution: <br>
$x \equiv 6  \mod 7$ <br> 
$x \equiv 1  \mod 11$ <br>
$\equiv$<br>
$x \equiv ?  \mod 77$ <br>
-----<br>
$N_{1} = 11$<br>
$n_{1} =$ ? <br>
$11 * n_{1} + (- z_{1}) * 7 = 1$ <br>
$11 * 2 - 1 = 3 * 7$ --- BI.<br>
$n_{1} = 2$<br>
$a_{1}N_{1}n_{1} = 6 * 11 * 2 = 132$<br>
-----<br>
$N_{2} = 7$ <br>
$n_{2} =$ ? <br>
$7 * n_{2} + (- z_{2}) * 11 = 1$ <br>
$7 * 8 - 1 = 5 * 11$ <br>
$n_{2} = 8$<br>
$a_{2}N_{2}n_{2} = 1 * 7 * 8 = 56$<br>
-----<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ <br>
-><br>
$x \equiv 132 + 56 (\mod 77)$ <br>
-><br>
$x \equiv 34 (\mod 77)$ <br>
----------<br>

4th solution: <br>
$x \equiv 6  \mod 7$ <br> 
$x \equiv 10  \mod 11$ <br>
$\equiv$<br>
$x \equiv ?  \mod 77$ <br>
-----<br>
$N_{1} = 11$<br>
$n_{1} =$ ? <br>
$11 * n_{1} + (- z_{1}) * 7 = 1$ <br>
$11 * 2 - 1 = 3 * 7$ --- BI.<br>
$n_{1} = 2$<br>
$a_{1}N_{1}n_{1} = 6 * 11 * 2 = 132$<br>
-----<br>
$N_{2} = 7$ <br>
$n_{2} =$ ? <br>
$7 * n_{2} + (- z_{2}) * 11 = 1$ <br>
$7 * 8 - 1 = 5 * 11$ <br>
$n_{2} = 8$<br>
$a_{2}N_{2}n_{2} = 10 * 7 * 8 = 560$<br>
-----<br>
$x \equiv a_{1}N_{1}n_{1} + a_{2}N_{2}n_{2} (\mod m_{1} * m_{2})$ <br>
-><br>
$x \equiv 132 + 560 (\mod 77)$ <br>
-><br>
$x \equiv 76 (\mod 77)$<br>  
----------<br>

Then to resume: <br>
-----<br>
$x \equiv 1  \mod 7$ <br>
$x \equiv 1  \mod 11$ <br>
->
$x \equiv 1 (\mod 77)$ <br>
-----<br>
$x \equiv 1  \mod 7$ <br>
$x \equiv - 1  \mod 11$ <br>
->
$x \equiv 43 (\mod 77)$ <br>
-----<br>
$x \equiv - 1  \mod 7$ <br>
$x \equiv 1  \mod 11$ <br>
->
$x \equiv 34 (\mod 77)$ <br>
-----<br>
$x \equiv - 1  \mod 7$ <br>
$x \equiv - 1  \mod 11$ <br>
->
$x \equiv - 1 (\mod 77)$ <br>
-----<br>

Indeed, recalling $x^{2} \equiv 1 \mod 77$:

$1^{2} \equiv 1 \mod 77$ <br>
$43^{2} \equiv 1 \mod 77$ <br>
$34^{2} \equiv 1 \mod 77$ <br>
$76^{2} \equiv 1 \mod 77$

These 4 numbers obtained are called the square roots of unity of $x^{2} \equiv 1 \mod 77$. <br>
</p>
