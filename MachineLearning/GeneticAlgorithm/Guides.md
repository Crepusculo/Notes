# Genetic Algorithm 入门知识梳理

标签（空格分隔）： Algorithm Algorithm-GA MachineLearning

[TOC]

---

# Wiki
遗传算法（genetic algorithm GA） 是计算数学中用于解决最佳化的搜索算法，是进化算法的一种。进化算法最初是借鉴了进化生物学中的一些现象而发展起来的，这些现象包括**遗传** ( Inheritance ) 、**突变** ( Mutation ) 、**自然选择** （ Selection ) 以及**杂交** ( Crossover ) 等。

遗传算法通常实现方式为一种计算机模拟。

对于一个最优化问题，一定数量的**候选解**（称为个体）可抽象表示为**染色体**，使种群向更好的解进化。
> In a genetic algorithm, a population of candidate solutions ( called individuals, creatures, or phenotypes ) to an optimization problem is evolved toward better solutions.

> Each candidata solution has a set of properties ( its chromosomes or genotype ) witch can be mutated and altered;



传统上，解用二进制表示（即0和1的串），但也可以用其他表示方法。
> Traditionally, solutions are represented in binary as strings  of 0s and 1s, but other encodeings are also possible.

进化从完全随机个体的种群开始，之后一代一代发生。在每一代中评价整个种群的适应度，从当前种群中随机地选择多个个体（基于它们的适应度），通过自然选择和突变产生新的生命种群，该种群在算法的下一次迭代中成为当前种群。
> The evolution usually starts from a poplution of randomly generated individuals and is an iterative process, with the populaition in each iteration called a *generation*.
In each *generation*, the fitness of every individual in the population is evaluated; the fitness is usually the value of the object function in the optimization problem being solved. The more fit individuals are stochastically selected from the current population, and each individual's genome is modified ( recombined and possibly randomly mutated ) to form a new generation.The new *generation* of candidate solutions is then used in the next iteration of the algorithm.

通常, 算法的终止条件有以下原因:
1. 达到进化次数限制
2. 适应度已经达到饱和 / 一个个体已经满足最优值条件, 继续进化不会产生适应度更好的个体
3. ( 人为干预 )
4. ( 计算耗费资源限制 ) ( 例如计算时间, 计算占用的内存等 )

> Commonly, the algorithm terminates when either a maximum number of generations has been produced, or a satisfactory fitness level has been reached for the population.

一个典型的遗传算法需要:
1. 一个解决域的**基因表示**
2. 一个解决域的**适应度函数**
> A typical genetic algorithm requires:
    1. a **genetic representation** of the solution domain.
    2. a **fitness function** to evaluate the solution domain.

|GA |    params mean                      | explain  |  |
|:-:| :-----------------------------------| :------  |
|P  | population size                     | 种群规模 | 种群中染色体个体的数目
|l  | string length                       | 字串长度 | 个体中染色体的长度
|pc | probability of performing crossover | 交叉概率 | 控制着交叉算子的使用频率
|pm | probability of mutation             | 变异概率 | 控制着变异算子的使用频率
|t  | termination criteria                | 中止条件 |

一串由01组成的字符串可以视作一个标准的遗传算法。其它形式的数组和数据结构基本上也适用。
遗传算法中主要通过**交配(交叉操作)**来完成修正工作。

` Varible length representations ` -> `Genetic programming`
` Graph-form representations     ` -> `Evolutionary programming`
` A mix of both linear chromosomes and trees ` -> `Gene expression programming`

>A standard representation of each candidate solution is as an array of bits.Arrays of other types and structures can be used in essentially the same way.The main property that makes these genetic representations convenient is that their parts are easily aligned due to their fixed size, which facilitates simple **crossover** operations.
Varible length representations are explored in genetic programming and graph-form representations are explored in evolutionary programming; a mix of both linear chromosomes and trees is explored in gene expression programming.


---

# Wish you have fun in biology !

## 交叉 Crossover
杂交操作也是遗传算法的核心部分

杂交操作就是将两个父本染色体上的基因进行重新组合分配，从而产生下一代个体的过程，通过杂交可能会将两个父本的优势基因组合在一起，产生适应度更高、更接近最优解的新个体。通常杂交算法和基因的编码方式有关，当前采用最多的是二进制编码方式，二进制编码的主要杂交算法有：

### 单点杂交
这种杂交方式是当前使用最多的杂交算法。单点杂交的主要过程是：首先在染色体上随机选择一个交换点；然后确定是在交换点前面部分或者后面部分的基因进行交换；最后根据前面的原则将两父本的染色体基因进行交换重组，从而形成了新的个体，即下一代个体。如有两个父本染色体序列10010|111和00101|010，其中“|”表示交换点，按照父本染色体的交换点前部分交换的原则，产生的新得下一代个体的染色体分别是00101|111和10010|010。
### 多点杂交
多点杂交算法就是指定了多个交换点用于父本的基因交换重组，具体的执行过程与单点杂交算法类似。
### 均匀杂交
上述的两种杂交算法存在杂交的染色体中某些部分的基因会被过早地舍弃，这是由于在交换前它们必须确定交换父本染色体交换位前面还是后面的基因，从而对于那些无关的基因段在交换前就已经收敛了。均匀杂交算法（Uniform Crossover）就可以解决上述算法的这种局限性，该算法的主要过程如下：首先随机选择染色体上的交换位；然后随机确定交换的基因是父本染色体上交换位的前部分基因还是后部分还部分基因；最后对父本染色体的基因进行重组从而产生新的下一代个体。
### 洗牌杂交
该杂交算法的最大特点是通常将染色体的中点作为基因的交换点，即从每个父本中取它们一般的基因重组成新的个体。另外针对于实值编码方式，还有离散杂交、中间杂交、线性杂交和扩展线性杂交等算法。
## 突变 Mutation


---



---


# For Fun

http://rednuht.org/genetic_cars_2/

http://boxcar2d.com/index.html

http://rednuht.org/genetic_walkers/

http://rednuht.org/geneticat/

https://github.com/be5invis/sfdhanautohint


---
`Resource` : http://michaelxiang.me/2015/12/24/algorithm-GA-basic/
`Author` : Michael翔

---
`Resource` : https://en.wikipedia.org/wiki/Genetic_algorithm

---
