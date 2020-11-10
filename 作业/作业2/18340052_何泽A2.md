<h1 align=center>AI (Fall 2020) – Assignment 2</h1>

<h1 align=center>CSP and KR</h1>

<h1 align=center>何泽  18340052</h1>

## Ⅰ

> Provide formulations for each of the following problems as CSPs: specify the variables, domains and constraints.
>
> 1.  Magic square: An order 3magic square is a 3×3 square grid filled with distinct positive integers in the range 1, 2, ..., 9 such that the sums of the integers in each row, column and diagonal are equal.
> 2. Independent set: Given a graph and a number k, find an independent set of size k, that is, a set of k vertices, no two of which are adjacent.
> 3. Crypto-arithmetic puzzle: $INT × L = AAAI$. We want to replace each letter by a different digit so that the equation is correct.

1. 变量：若i代表行号，j代表列号，令第$(i, j)$个格填入的数字为变量$V_{ij}$，其中，$i, j ∈ \{1, 2, 3\}$。

    论域：每个变量的论域均为$\{1,2,...,9\}$

    限制条件：$\forall i\in \{1,2,...,9\},\sum_{n=1}^{9}V_{in}=\sum_{n=1}^{9}V_{ni}=\sum_{n=1}^{9}V_{nn}$ ，且$A_{ij}$ 各不相等

2. 设变量$V_1, V_2, . . . , V_k$为独立集中的k个元素，每一个$V_i$的论域均为图的所有顶点V ，限制条件为：

    $C(V1,V2,...,Vk)$满足$∀Vi,Vj(i,j∈{1,...,k}∧i \not= j)$，$V_i$与$V_j$不相邻，且$V_i$ 各不相等

3. 设变量为$V_I,V_N,V_T,V_L,V_A$ ，每一个变量论域为$\{0,1,2,...,9\}$，限制条件：

    $C(V_I,V_N,V_T,V_L,V_A)$ 满足：
    
    $V_T\times V_L+10\times V_N\times V_L+100\times V_I \times V_L=1000\times V_A+100\times V_A+10\times V_A+V_I $

## Ⅱ

> Consider the following CSP with binary constraints. There are 4 variables: A, B, C, D with their respective domains:
>
> $D_A = \{1,2,3,4\}, D_B = \{3,4,5,8,9\}, D_C = \{2,3,5,6,7,9\}, D_D = \{3,5,7,8,9\}$. 
>
> The constraints are:
>
> - $C1 :A≥B$
>
> - $C2 : B > C \ \ or\ \  C − B = 2$
>
> - $C3 : C\not= D$
>
> 1.  Find the first solution by using the Forward Checking algorithm with the MRV heuristics, *i.e.*, always choose the variable with smallest remaining number of elements in the domain to instantiate, breaking ties in the alphabetic order. Assign values in the current domain of each variable in increasing order. At each node indicate:
>
>       i. The variable being instantiated and the value being assigned to it.
>
>      ii. The CurDom for each variable.
>
>     iii. Mark any node with an empty CurDom with DWO.
>
> 2. Enforce GAC on the constraints and give the resultant variable domains. You should show which values of a domain are removed at each step, and which ajrc is responsible for removing the value. After this first step, use the GAC algorithm to find the first solution.

1. 

<img src="/Users/heze/Downloads/IMG_7028B413140D-1.jpeg" alt="IMG_7028B413140D-1" style="zoom:80%;" />

2. 

<img src="/Users/heze/Downloads/IMG_CEEDE8F745E1-1.jpeg" alt="IMG_CEEDE8F745E1-1" style="zoom:80%;" />

## Ⅲ 

> Consider the following facts about the Elm Street Bridge Club:
>
> Joe, Sally, Bill, and Ellen are the only members of the club. Joe is married to Sally. Bill is Ellen's brother. The spouse of every married person in the club is also in the club.
>
> From these facts, most people would be able to determine that Ellen is not married.
>
> 1. Represent these facts as sentences in FOL, and show semantically that by themselves they do not entail that Ellen is not married.
> 2. Write in FOL some additional facts that most people would be expected to know, and show that the augmented set of sentences now entails that Ellen is not married.

1. 记Joe, Sally, Bill和 Ellen分别为J,S,B和E，谓词A(X)表示X在俱乐部中，B(X,Y)表示X和Y是伴侣，C(X,Y)表示X是Y的兄弟，则有：

    $A(J), A(S),A(B),A(E),\ B(J,S),C(B,E) $

    $\forall x \notin\{J,S,B,E\},\lnot A(x)$

    $\forall x(\ \ (A(x)→\lnot(∃y,A(y) \and B(x,y))\ \ \or\ \ ∃y(A(y)\and B(x,y)\ \ )$

    题目中没有说兄妹之间不能结婚，故无法确定Ellen没有结婚。

2. 添加的额外的事实：

    > 自己不能和自己结婚，兄妹不能结婚，且一个人只能和一个人结婚

    $\forall x,\lnot B(x,x)$

    $\forall x\forall y,\ C(x,y)\to\lnot B(x,y)$

    $\forall x\forall y,B(x,y)\to \forall z(\lnot B(x,z)\and \lnot B(y,z))$

    证明：

    令D(x)表示x已婚

    $A(E),\ \ \forall x(\ \ (A(x)→\lnot(∃y,A(y) \and B(x,y))\ \ \or\ \ ∃y(A(y)\and B(x,y)\ \ )$

    $\Rightarrow\ \exists y(A(y)\and(B(E,y)\or \lnot D(E))$

    $B(J,S),\ \ \forall x\forall y(B(x,y)\to \forall z(\lnot B(x,z)\and \lnot B(y,z))) $

    $\Rightarrow \lnot B(J,E)\ \and\ \lnot B(S,E)$

    $C(B,E),\ \forall x\forall y,\ C(x,y)\to\lnot B(x,y)$

    $\Rightarrow \lnot B(B,E)$

    $\forall x,\lnot B(x,x)$

    $\Rightarrow \lnot B(E,E)$

    综上可得 $\lnot D(E)$ ，即Ellen未婚。

## Ⅳ

> Consider the following formulae asserting that a binary relation is symmetric, transitive, and serial:
>
> ​	$S1 : ∀x∀y(P(x,y) → P(y,x))$
>
> ​	$S2 :∀x∀y∀z(P(x,y)∧P(y,z)→P(x,z))$
>
> ​	$ S3 : ∀x∃yP (x, y)$
>
> Prove by resolution that
> $$
> S1 ∧ S2 ∧ S3 \models ∀xP (x, x)
> $$
> In other words, if a binary relation is symmetric, transitive and serial, then it is reflexive.

S1 : $∀x∀y(P(x,y) → P(y,x))\ \ \Rightarrow\ \ ∀x∀y(\lnot P(x,y) \or P(y,x))\ \ \Rightarrow\ \ \lnot P(x,y)\or P(y,x)$

​	**1		$(\lnot P(x,y), P(y,x))$**

S2：$∀x∀y∀z(P(x,y)∧P(y,z)→P(x,z))\ \ \Rightarrow\ \ ∀x∀y∀z(\lnot (P(x,y)∧P(y,z))\or P(x,z))$

​		$\Rightarrow\ \ ∀x∀y∀z(\lnot P(x,y)\or \lnot P(y,z)\or P(x,z))\ \ \Rightarrow\ \ \lnot P(m,n)\or \lnot P(n,k)\or P(m,k)$

​	**2		$\lnot P(m,n), \lnot P(n,k), P(m,k)$**

 S3 : $∀x∃yP (x, y)\ \ \Rightarrow\ \ ∀p∃qP (p, q)\ \ \Rightarrow\ \ \forall p\ P(p,f(p))$

​	**3		$P(p,f(p))$**

$∀xP (x, x)\ \ \Rightarrow\ \ \exists x\lnot P(x,x)\ \ \Rightarrow\ \ \exists a\lnot P(a,a)$

​	**4		$\lnot P(a,a)$**		

​	**5**		$R[2c,4]\{m=a,k=a\}(\lnot P(a,n),\lnot P(n,a))$

​	**6**		$R[1b,5b]\{y=n,x=a\}(\lnot P(a,n))$

​	**7**		$R[3,6]\{p=a,n=f(p)\}()$