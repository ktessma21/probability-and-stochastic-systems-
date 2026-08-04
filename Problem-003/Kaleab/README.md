# Problem
Three playes, A, B, C, each choose a real number betwenn 0 and 100, inclusive. The player who chooses the largest number pays each of the other two players an amount equal to that player's choosen number. Player A chooses first. Player B then sees A's choice before choosing their own. Both players are perfectly rational. Finally, Player C chooses uniformly at random from the integers 0 though 100<sup>1</sup>. Before the game begins, A and B know that C will choose uniformly at random. 

What number should A choose to maximize their expected payoff?

--- 
# Solution

**Note: to make my life a little nicer I chose $c$ to be continously uniform from 0 to 100. I think it shouldn't affect the answer**

Let players $A$, $B$, $C$ pick values $a$, $b$, $c$, with $c \sim \mathrm{Unif}(0, 100)$.

Since player $B$ moves after player $A$, it makes sense to first find $B$'s optimal
strategy: $B$ maximizes their expected payoff given what $A$ picked.

### Optimal Strategy for Player B

Write $E_B(b \mid a)$ for the expected payoff of player $B$ as a function of the
choice $b$, given that player $A$ picked $a$.

We can split the choice of $b$ into two cases.<sup>2</sup>

#### Case 1: $b > a$

$$
P(c > b) = 1 - \frac{b}{100}, \qquad P(c < b) = \frac{b}{100}
$$

$$
\begin{aligned}
E_B(b \mid a)
  &= P(c > b) \cdot b \;-\; P(c < b) \cdot (a + c) \\
  &= \left(1 - \frac{b}{100}\right) b \;-\; \frac{b}{100}(a + c) \\
  &= b - \frac{b^2 + ab + bc}{100}
\end{aligned}
$$

#### Case 2: $b < a$ <sup>3</sup>

$$
E_B(b \mid a) = P(c > a) \cdot b + P(c < a) \cdot b = b
$$

This case has the better payoff, even though player $B$ picks a value $b < a$.

#### Choosing $b$

The goal is to maximize $E_B(b \mid a) = b$. Since the payoff is increasing in $b$ but
the case requires $b < a$, player $B$ picks a value as close to $a$ as possible from
below. So we can take $b = a$.<sup>4</sup>

### Optimal Strategy for Player A

$E_A(a)$ is the expected payoff of player A as a function of what it choose given what it chooses. 

To simplify this, we need to use a common property that $E_A(a) = E(E_A(a | c)).$ This expression might be a bit confusing. The inner expectation if over values of $a$ given value $c$. And the outer expecetation is over different values of $c$. 

We know $b$ is almost $c$ but a bit lower.

$$
E_A(a \mid c) = P(a < c) * a - P(a > c) (b + c)
$$

$$
P(c > a) = 1 - \frac{a}{100}, \qquad P(c < a) = \frac{a}{100}
$$

$$
\begin{aligned}
E_A(a \mid c) 
  &= P(a < c) * a - P(a > c) (b + c) \\
  &= \left(1 - \frac{a}{100}\right) * a - \frac{a}{100}(b + c) \\
  &= a - \frac{a^2 - ab - ac}{100}
\end{aligned}
$$

Probabilty density function of $c$, $f(c) = \frac{1}{100}$.

$$
\begin{aligned}
E_A(a) 
  &= E(E_A(a | c)) \\
  &= E\left(a - \frac{a^2 + ab + ac}{100}\right) \\
  &= \int_{0}^{100}{\left(a - \frac{a^2 + ab + ac}{100}\right) * f(c) dc} \\
  &= \frac{1}{100} \left[ac - \frac{a^2c + abc}{100} - \frac{ac^2}{200}\right]_{c=0}^{c=100} \\
  &= \frac{1}{100} \left(100a - \frac{100a^2 + 100ab}{100} - \frac{100a}{2}\right) \\
  &= a - \frac{a^2 + ab}{100} - \frac{a}{2} \\
  &= \frac{a}{2} - \frac{2a^2}{100} \\
\end{aligned}
$$

#### Differenciating $E_A(a)$
$$
\frac{d E_A(a)}{da} = \frac{1}{2} - \frac{4a}{100} = 0 \implies \boxed{a=\frac{50}{4} = 12.5}
$$

**$12.5$** is values player A should pick to maximize its payoff

### Simulation can be found [here](/Problem-003/Kaleab/simulation.ipynb)
---

### Notes
<sup>1</sup> I don't know why the problem decided to make $c$ a discrete variable (integer). It would have been much cleaner as a real number from 0 to 100. I don't think it will change the answer much.

<sup>2</sup> This step of splitting into two cases wasn't intuitive for me, and I don't
quite get it yet. I wonder if it is accurate and it might cause any problems.

<sup>3</sup> It is not clear who pays whom if there is equality among $a$, $b$, $c$.
But my logic is that since $a$ and $b$ are continuous values, the probability of that
happening is $0$.

<sup>4</sup> $b = a - 0.0000000000001$ lol
