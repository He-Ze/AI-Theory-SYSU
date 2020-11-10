<h1 align=center>AI (Fall 2020) – Assignment 3</h1>

<h1 align=center>Planning and Uncertainty</h1>

<h1 align=center>何泽  18340052</h1>

## Ⅰ

> Shakey the robot wakes up in a dark room r1, there is a light bulb but the switch is turned off. After inspection, she finds out there are another two rooms r2, r3 next to this one, where r2 contains a box b1 and r3 contains a box b2. To light up the bulb, box b1 must be in room r1 and b2 in r2. The domain of objects in this problem is thus,$ \{shakey, r1, r2, r3, b1, b2\}$. The robot Shakey can achieve her goal using the following 3 actions:
>
> - $walkTo(loc1, loc2)$: Shakey walks from location loc1 to loc2 where the two locations are adja- cent.
> - $push(box, loc1, loc2)$: Shakey pushes the box from loc1 to loc2 where the two locations are adjacent.
> - $turnOn$: Shakey turns on the light bulb in room r1, only if the boxes are in their correct posi- tions.
>
> The descriptions would require the two fluents and one predicate:
>
> - $lightOn(s)$: in situation s, the light bulb in room r1 is on.
> - $at(obj, loc, s)$: in situation s, the object obj (box or shakey) is in the location $loc (r1, r2\ or\ r3)$. 
> - $adj(l1, l2)$: the two locations are adjacent.
>
> Using the situation calculus, help Shakey to see the light.
>
> 1. An object cannot be in two different locations in the same situation. Formalize this axiom.
>
>     **(Hint: quantify over situation $s$, object $o$, and two locations $l_1$ and $l_2$.)**
>
> 2. Write a sentence describing the initial situation S0; Write a sentence of the form $∃s.φ(s)$ that asserts the existence of the final goal situation using the fluents. (you are not required to provide the adjacency of the rooms)
>
> 3.  Write the precondition and effect axioms for the actions.
>
> 4. Write the goal situation $σ$ as a ground situation term, using as few actions as possible. **(Hint:Review the definition of a term; The do(a, s) function is your friend in situation calculus.)**
>
> <img src="/Users/heze/Library/Application Support/typora-user-images/image-20201108201123859.png" alt="image-20201108201123859" style="zoom: 40%;" />

1.  $\forall s\forall o \forall l_1 \forall l_2\ ,\ at(o,l_1,s)\and at(o,l_2,s)\to l_1=l_2$

2. 

    - $initial\ situation\ S_0$:

        $at(shakey,r_1,s_0)\and at(b_1,r_2,s_0)\and at(b_2,r_3,s_0)\and \lnot lightOn(s_0)$

    -  $final \ goal \ situation$:

        $at(b_1,r_1,s)\and at(b_2,r_2,s)\and lightOn(s)$

3. 

    - $walkTo(loc1, loc2)$

        $precondition:\ \forall loc_1\forall loc_2,at(shakey,loc_1,s)\and adj(loc_1,loc_2)$

        $effect:\ at(shakey,loc_2,do(walkTo(loc1, loc2)),s)$

    - $push(box, loc1, loc2)$

        $precondition:\forall loc_1\forall loc_2,at(shakey,loc_1,s)\and at(box,loc_1,s)\and adj(loc_1,loc_2)$

        $effect:\ at(shakey,loc_2,do(push(box, loc1, loc2)),s)\and at(box,loc_2,do(push(box, loc1, loc2)),s) $

    - $turnOn$

        $precondition:\ at(b_1,r_1,s)\and at(b_2,r_2,s)\and \lnot lightOn(s)$

        $effect:lightOn(do(turnOn),s)$

4. $σ=do(walkTo(r_1,r_2),do(walkTo(r_2,r_3),do(push(b_2,r_3,r_2),do(push(b_1,r_2,r_1),do(turnOn),s_0)))))$

## Ⅱ

> Consider the tower of Hanoi problem. There are 3 disks d1, d2, d3 (where di is smaller than dj for i < j) and 3 pegs p1, p2, p3. At first the 3 disks are stacked orderly in the first peg, and you are asked to move the entire stack to the third one. There are three predicates:
>
> - $clear(x)$: either peg x is clear or there is no disk on top of disk x.
> - $on(x,y$): diskxisondisky,ordiskxisonpegy.
> - $smaller(x, y$): disk x is smaller than disk y, or x is a disk and y is a peg.
>
> Suppose we have an enhanced robotic arm that is also able to move two consecutive disks in a single action:
>
> - $move(x, a, b)$: move disk x from the peg/disk a to the peg/disk b.
> - $moveT wo(x, y, a, b)$: move a consecutive stack of two disks x, y from the peg/disk a to the peg/disk b.
>
> With this enhancement, complete the following tasks:
>
> 1. Write the STRIPS representation of actions, the initial KB and the goal.
>
> 2. Use reachability analysis to compute the heuristic value for the initial state. Draw the state and action layers. For each call of CountActions, indicate the values of G, G~P~ , G~N~ and A.
>
> **Note: Assume that the axioms of all smaller relations of the disks and pegs are given, thus there is no need to specify these relations in the initial KB, goal and the state layers.**
>
> <img src="/Users/heze/Library/Application Support/typora-user-images/image-20201108201644496.png" alt="image-20201108201644496" style="zoom: 40%;" />

1.  

    - initial KB

        $KB=\{clear(d_1),clear(p_2),clear(p_3),on(d_1,d_2),on(d_2,d_3),on(d_3,p_1)\}$

    - $move(x, a, b)$:

        - $Pre :\{clear(x),clear(b),on(x,a), smaller(x,b)\}$
        - $Add:\{on(x,b),clear(a) \}$
        - $Del:\{clear(b),on(x,a) \}$

    - $moveT wo(x, y, a, b)$: 

        - $Pre:\{clear(x),clear(b),on(x,y),on(y,a),smaller(y,b) \}$
        - $Add:\{on(y,b),clear(a) \}$
        - $Del:\{clear(b),on(y,a) \}$

    - Goal:

        $Goal=\{clear(p_1),clear(p_2),clear(d_1),on(d_1,d_2),on(d_2,d_3),on(d_3,p_3) \}$

2.  

$S_0:\{clear(d_1),clear(p_2),clear(p_3),on(d_1,d_2),on(d_2,d_3),on(d_3,p_1) \}$

$A_0:\{move(d_1,d_2,p_2) \}$

$S_1:\{clear(d_1),clear(p_2),clear(p_3),on(d_1,d_2),on(d_2,d_3),on(d_3,p_1), on(d_1,p_2),clear(d_2) \}$

$A_1:\{moveTwo(d_2,d_3,p_1,p_3),move(d_1,p_2,d_2) \}$

$S_2:\{clear(d_1),clear(p_2),clear(p_3),on(d_1,d_2),on(d_2,d_3),on(d_3,p_1), on(d_1,p_2),clear(d_2),on(d_3,p_3),clear(p_1),on(d_1.d_2),clear(p_2) \}$

可以看出$Goal⊂S_2$ ，图示如下：

<img src="/Users/heze/Library/Mobile Documents/com~apple~CloudDocs/大三上/人工智能/作业/作业3/1.jpeg" alt="1" style="zoom:40%;" />

- 由S~2~有：

    $G=\{clear(p_1),clear(p_2),clear(d_1),on(d_1,d_2),on(d_2,d_3),on(d_3,p_3) \}$

    $G_P=\{clear(p_2),clear(d_1),on(d_1,d_2),on(d_2,d_3)\}$

    $G_N=\{clear(p_1),on(d_3,p_3) \}$

    $A=\{[clear(d_2),clear(p_3),on(d_2,d_3),on(d_3,p_1)]moveTwo(d_2,d_3,p_1,p_3)[clear(p_1),on(d_3,p_3)] \}$

    $G_1=G_P∪Pre(A)=\{clear(p_2),clear(d_1),on(d_1,d_2),on(d_2,d_3),clear(d_2),clear(p_3),on(d_3,p_1) \}$

    $CountActions(G,S_2)=1+CountActions(G_1,S_1)$

- 由S~1~有：

    $G_P=\{clear(p_2),clear(d_1),on(d_1,d_2),on(d_2,d_3),clear(p_3),on(d_3,p_1) \}$

    $G_N=\{clear(d_2) \}$

    $A=\{[clear(d_1),clear(p_2),on(d_1,d_2)] move(d_1,d_2,p_2)[on(d_1,p_2),clear(d_2)] \}$

    $G_2=G_P∪Pre(A)=\{clear(p_2),clear(d_1),on(d_1,d_2),on(d_2,d_3),clear(p_3),on(d_3,p_1) \}$

    $CountActions(G_1,S_1)=1+CountActions(G_2,S_0)$

于是可得：
$$
CountActions(G,S_2)=1+1+0=2
$$

## Ⅲ

> Consider the following example: An addition to games is a possible cause of a student getting a low score in the final exam and it could also lead to lack of physical exercises. In turn, either the low score or the lack of exercises could render a student unpopular among classmates. Besides, the low score in the final exam might attribute to the rejection of scholarship application.
>
> 1. Represent these casual links in a belief network. Let $a$ stand for addition to games, $b$ for lack of exercises, $c$ for low score in the final exam, $d$ for being unpopular among classmates, and $e$ for rejection of scholarship application.
>
> 2. Give an example of an independence assumption that is implicit in this network.
>
> 3. Suppose the following probabilities are given:
>
>     <img src="/Users/heze/Library/Application Support/typora-user-images/image-20201108201746327.png" alt="image-20201108201746327" style="zoom:45%;" />
>
>     and assume that it is also given that some student is popular among classmates but has no schol- arship. Calculate joint probabilities for the eight remaining possibilities (that is according to whether a,b, and c are true or false)
>
> 4. According to the numbers given, the a priori probability that the student is addicted to games is 0.2. Given that the student has no scholarship but is popular among classmates, are we now more or less inclined to believe that the student has game addiction? Explain.

1.  

    <img src="/Users/heze/Library/Application Support/typora-user-images/image-20201109105610562.png" alt="image-20201109105610562" style="zoom:35%;" />

2.  若给定b,c则有d与a,e独立，即：
    $$
    P(d|a,b,c,e)=P(d|b,c)
    $$

3.  

    $P(a,b,c,\lnot d,e) = P(a) P(b\mid a) P(c\mid a) P(\lnot d\mid b,c) P(e\mid c)=0.2\times0.7\times0.2\times0.2\times0.7=0.00392$

    $P(a,b,\lnot c,\lnot d,e)  =  P(a) P(b\mid a) P(\lnot c\mid a) P(\lnot d\mid b,\lnot c) P(e\mid \lnot c)  =0.2\times0.7\times0.8\times0.3\times0.6=0.02016$

    $P(a,\lnot b,c,\lnot d,e)  =  P(a) P(\lnot b\mid a) P(c\mid a) P(\lnot d\mid \lnot b,c) P(e\mid c)  =0.2\times0.3\times0.2\times0.3\times0.7=0.00252$

    $P(a,\lnot b,\lnot c,\lnot d,e)  =  P(a) P(\lnot b\mid a) P(\lnot c\mid a) P(\lnot d\mid \lnot b,\lnot c) P(e\mid \lnot c)  = 0.2\times0.3\times0.8\times0.95\times0.6=0.02736$

    $P(\lnot a,b,c,\lnot d,e)  =  P(\lnot a) P(b\mid \lnot a) P(c\mid \lnot a) P(\lnot d\mid b,c) P(e\mid c)  =0.8\times0.2\times0.05\times0.2\times0.7=0.00112$

    $P(\lnot a,b,\lnot c,\lnot d,e)  =  P(\lnot a) P(b\mid \lnot a) P(\lnot c\mid \lnot a) P(\lnot d\mid b,\lnot c) P(e\mid \lnot c)  =0.8\times0.2\times0.95\times0.3\times0.6=0.02736$

    $P(\lnot a,\lnot b,c,\lnot d,e)  =  P(\lnot a) P(\lnot b\mid \lnot a) P(c\mid \lnot a) P(\lnot d\mid \lnot b,c) P(e\mid c)  =0.8\times0.8\times0.05\times0.3\times0.7=0.00672$

    $P(\lnot a,\lnot b,\lnot c,\lnot d,e)  =  P(\lnot a) P(\lnot b\mid \lnot a) P(\lnot c\mid \lnot a) P(\lnot d\mid \lnot b,\lnot c) P(e\mid \lnot c)  =0.8\times0.8\times0.95\times0.95\times0.6=0.34656$ 

    由此可以计算 $P(\lnot d,e)=\sum_{a,b,c} P(a,b,c,\lnot d,e)=0.43572 $

    于是可得：

    $P(a,b,c|\lnot d,e) =\frac{P(a,b,c,\lnot d,e) }{P(\lnot d,e)}=0.008997$

    $P(a,b,\lnot c|\lnot d,e) =\frac{P(a,b,\lnot c,\lnot d,e)}{P(\lnot d,e)}=0.046268$

    $P(a,\lnot b,c|\lnot d,e) =\frac{P(a,\lnot b,c,\lnot d,e)}{P(\lnot d,e)}=0.005784$

    $P(a,\lnot b,\lnot c|\lnot d,e) =\frac{P(a,\lnot b,\lnot c,\lnot d,e)}{P(\lnot d,e)}=0.062793$

    $P(\lnot a,b,c|\lnot d,e) =\frac{P(\lnot a,b,c,\lnot d,e)}{P(\lnot d,e)}=0.002570$

    $P(\lnot a,b,\lnot c|\lnot d,e)=\frac{P(\lnot a,b,\lnot c,\lnot d,e) }{P(\lnot d,e)}=0.062793$

    $P(\lnot a,\lnot b,c|\lnot d,e) =\frac{P(\lnot a,\lnot b,c,\lnot d,e)}{P(\lnot d,e)}=0.015423$

    $P(\lnot a,\lnot b,\lnot c|\lnot d,e) =\frac{P(\lnot a,\lnot b,\lnot c,\lnot d,e) }{P(\lnot d,e)}=0.795373$
4. 

    $P(a,\lnot d,e)=\sum_{b,c}P(a,b,c,\lnot d,e)=0.05396$

    由贝叶斯公式可得：$P(a|\lnot d,e)=\frac{P(a,\lnot d,e)}{P(\lnot d,e)}=\frac{0.05396}{0.43572}=0.123841<P(a)=0.2$

    故概率降低。

## Ⅳ

> Consider the following belief network:
>
> <img src="/Users/heze/Library/Application Support/typora-user-images/image-20201108201901555.png" alt="image-20201108201901555" style="zoom:45%;" />
>
> 1. Compute $P (e) $ using VE. You should first prune irrelevant variables. Show the factors that are created for a given elimination ordering.
> 2. Supposed you want to compute $P(e|¬f)$ usingVE. How much of the previous computation can be reused? Show the factors that are different from those in part (a)

1. 相关变量：a,b,c,e  无关变量：d,f  令A，B，C，E的CPT分别为$f_1(A),f_2(B),f_3(A,B,C),f_4(C,E)$ ，按照A，B，C的顺序消除

    $f_5(B,C)=\sum_a f_1(a)f_3(a,B,C)=\begin{cases}0.16&{c,b}\\0.76&c,\lnot b\\0.04&\lnot c,b\\0.04&\lnot c,\lnot b\end{cases}$ 

    $f_6(C)=\sum_b f_2(b)f_5(b,C)=\begin{cases}0.64&c\\0.36&\lnot c\end{cases}$
    
    $f_7(E)=\sum_c f_6(c)f_4(c,E)=\begin{cases}0.52&e\\0.48&\lnot e\end{cases}$
    
    故可得：$P(e)=0.52$

2. 相关变量：a,b,c,e,f  无关变量：d

    $f_1(A),f_2(B),f_3(A,B,C),f_5(B,C)$和$f_6(C)$这5个可以复用，不同的因子为：$f_9(C)$，$f_{10}(C,E)$，$f_{11}(E)$

    - 限制F为$\lnot f$ ,用$f_9(C)=f_8(C,\lnot f)=\begin{cases}0.8&c\\0.1&\lnot c\end{cases}$    代替$f_8(C,F)$

    - 消除$A,B$ 依次得到$f_5(B,C)$和$f_6(C)$（此处复用第一小题的结果）

    - $f_4(C,E),f_6(C),f_9(C)$相乘：
        $$
        f_{10}(C,E)=f_4(C,E)\times f_6(C)\times f_9(C)=\begin{cases}0.3584&{c,e}\\0.1536&c,\lnot e\\0.072&\lnot c,e\\0.0288&\lnot c,\lnot e\end{cases}
        $$

    - 消除C：
        $$
        f_{11}(E)=\sum_c f_{10}(c,E)=\begin{cases}0.3656&e\\0.1824&\lnot e\end{cases}
        $$
        

    - 归一：
        $$
        P(e\mid\lnot f)=\frac{0.3656}{0.3656+0.1824}=0.66715
        $$
        



