# Hill Climbing & Simulated annealing

Tags: Algorithm Algorithm-Greedy Algorithm-GA Algorithm-LocalSearch

---

<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [Hill Climbing & Simulated annealing](#hill-climbing-simulated-annealing)
- [Local Search](#local-search)
   - [局部搜索](#局部搜索)
   - [Description](#description)
   - [应用](#应用)
- [Hill Climbing](#hill-climbing)
- [Simulated annealing](#simulated-annealing)

<!-- /MDTOC -->






---

# Local Search
> **Local search** is a heuristic method for solving computationally hard optimization problems. Local search can be used on problems that can be formulated as finding a solution maximizing a criterion among a number of candidate solutions. Local search algorithms move from solution to solution in the space of candidate solutions (the search space) by applying local changes, until a solution deemed optimal is found or a time bound is elapsed.

> **Local search** is the use of specialized Internet search engines that allow users to submit geographically constrained searches against a structured database of local business listings.

`heuristic method` 启发式

## 局部搜索
+ 局部搜索是一种**元启发式算法**
+ 局部搜索从一个初始解出发，然后搜索解的邻域，如有更优的解则移动至该解并继续执行搜索，否则返回当前解。
+ 优点是简单、灵活及易于实现。
+ 缺点是容易陷入局部最优且解的质量与初始解和邻域的结构密切相关。
+ 常见的改进方法有模拟退火、禁忌搜索等。
+ 广泛应用于各种很难找到全局最优解的计算问题。

## Description

> Most problems can be formulated in terms of search space and target in several different manners. For example, for the *travelling salesman problem* a solution can be a cycle and the criterion to maximize is a combination of the number of nodes and the length of the cycle. But a solution can also be a path, and being a cycle is part of the target.

> A local search algorithm starts from a candidate solution and then iteratively moves to a neighbor solution. This is only possible if a neighborhood relation is defined on the search space. As an example, the neighborhood of a vertex cover is another vertex cover only differing by one node. For boolean satisfiability, the neighbors of a truth assignment are usually the truth assignments only differing from it by the evaluation of a variable. The same problem may have multiple different neighborhoods defined on it; local optimization with neighborhoods that involve changing up to $k$ components of the solution is often referred to as **k-opt**.

> Typically, every candidate solution has more than one neighbor solution; the choice of which one to move to is taken using only information about the solutions in the neighborhood of the current one, hence the name **local** search. When the choice of the neighbor solution is done by taking the one locally maximizing the criterion, the metaheuristic takes the name **hill climbing**. When no improving configurations are present in the neighborhood, local search is stuck at a **locally optimal point**. This local-optima problem can be cured by using restarts (repeated local search with different initial conditions), or more complex schemes based on iterations, like [iterated local search][1], on memory, like [reactive search optimization][2], on memory-less stochastic modifications, like [simulated annealing][3].

> Termination of local search can be based on a time bound. Another common choice is to terminate when the best solution found by the algorithm has not been improved in a given number of steps. Local search is an anytime algorithm: it can return a valid solution even if it's interrupted at any time before it ends. Local search algorithms are typically **approximation** or **incomplete algorithms**, as the search may stop even if the best solution found by the algorithm is not optimal. This can happen even if termination is due to the impossibility of improving the solution, as the optimal solution can lie far from the neighborhood of the solutions crossed by the algorithms.

> For specific problems it is possible to devise neighborhoods which are very large, possibly exponentially sized. If the best solution within the neighborhood can be found efficiently, such algorithms are referred to as [very large-scale neighborhood][4] search algorithms.

`formulated` $v.$ 制定 \ `in terms of` $prep.$ 就......而言 \ `manners` $n.$ 规则 \ `criterion (to sth)` $n.$ 标准 \
`hence` $adv.$ 于是 \ `metaheuristic` $adj. / n.$ 启发式 \ `configurations` $n.$ 配置 \ `stochastic` $adj.$ 随机\
`approximation` $n.$ 近似 \ `devise` $v.$ 设计 \ `exponentially` $adv.$ 指数级

## 应用
"Hong Kong hotels",
"Manhattan restaurants",
"Dublin car rental".
"Bellevue, WA"
"14th arrondissement"
"restaurant"
"nail salon"

---

# Hill Climbing


---

# Simulated annealing


  [1]: https://en.wikipedia.org/wiki/Iterated_local_search
  [2]: https://en.wikipedia.org/wiki/Reactive_search_optimization
  [3]: https://en.wikipedia.org/wiki/Simulated_annealing
  [4]: https://en.wikipedia.org/wiki/Very_large-scale_neighborhood_search
