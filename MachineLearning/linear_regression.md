
<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [Linear Regression with One Variable](#linear-regression-with-one-variable)
   - [Model Representation](#model-representation)
   - [The Hypothesis Function](#the-hypothesis-function)
   - [Cost Function](#cost-function)
   - [Gradient Descent](#gradient-descent)
   - [Gradient Descent for Linear Regression](#gradient-descent-for-linear-regression)
   - [What's Next](#whats-next)
         - [接下来干啥](#接下来干啥)

<!-- /MDTOC -->

# Linear Regression with One Variable
**单变量线性回归**


## Model Representation
**模型表示**


Recall that in **regression problems**, we are taking input variables and trying to map the output onto a **continuous** expected result function.
>回顾在"回归问题"里, 我们输入变量，试图把输出映射到一个**连续的**用于预测结果的函数里

Linear regression with one variable is also known as "univariate linear regression."
>单因子线性回归也被叫做单变量线性回归

Univariate linear regression is used when you want to predict a **single output** value from a **single input** value. We're doing **supervised learning** here, so that means we already have an idea what the input/output cause and effect should be.
>单因子线性回归被用于从 **单一**一个输入值 预测出 **单一**一个输出值。在此处使用监督学习，表明我们已经对于input/output的因果关系拥有了一个idea

## The Hypothesis Function
**假设函数**

Our hypothesis function has the general form:
>假设函数的一般形式：

$$h_{\theta}(x)=\theta_{0}+\theta_{1}x$$

We give to $h_{\theta}$ values for $\theta_{0}$ and $\theta_{1}$ to get our output '$y$'. In other words, we are trying to create a function called $h_{\theta}$ that is able to reliably map our input data (the $x$'s) to our output data (the $y$'s).

>为函数 $h_{\theta}$ 提供自变量 $\theta_{0}$ 和 $\theta_{1}$ 的值,从而得到输出值 $y$ 。换句话说，我们试图创建一个函数 $h_{\theta}$ 能够可靠地将我们的输入数据 $x$ 映射到输出数据 $y$ 。

Example:
>大栗子

| **x (input)** | **y (output)** |
|---|---|
| 0 | 4 |
| 1 | 7 |
| 2 | 7 |
| 3 | 8 |

Now we can make a random guess about our $h_{\theta}$ function: $\theta_{0}=2$ and $\theta_{1}=2$. The hypothesis function becomes $h_{\theta}(x)=2+2x$.
>现在我们可以随意猜猜 $h_{\theta}$ 函数: $\theta_{0} = 2$ 和 $\theta_1 = 2$ 。
那么现在假设函数变成了$h_{\theta}(x)= 2 + 2 x$。

So for input of 1 to our hypothesis, y will be 4\. This is off by 3.
>所以对着我们的假设输入一个1,$y$ 应该是4,与实际差值为3(?)

## Cost Function
**代价函数**

We can measure the accuracy of our hypothesis function by using a **cost function**. This takes an average (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's compared to the actual output y's.
>通过**代价函数cost function**来测量构建的假设函数hypothesis function的精密性。代价函数通过比较输入的x和实际输出的y,产生一个由所有假设函数的(魔改强化版的)平均值

$$J(\theta_{0},\theta_{1}) = \frac{1}{2m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})^2$$

To break it apart, it is $\frac{1}{2}\overline{x}$ where $\overline{x}$ is the mean of the squares of $h_{\theta}(x(i))-y(i)$, or the difference between the predicted value and the actual value.
>肢解一下，$\overline{x}$ 是指所有 $h_{\theta}(x(i))-y(i)$ 的平方，换句话说也就是预测值和实际值的不同 (?这句并没有怎么看懂)

This function is otherwise called the "Squared error function", or [Mean squared error](https://en.wikipedia.org/wiki/Mean_squared_error).The mean is halved $\frac{1}{2m}$ as a convenience for the computation of the gradient descent, as the derivative term of the square function will cancel out the 12 term.
>除此之外,这函数被称为"平方误差函数",也就是方差...因为平方函数的导数项可以消除$\frac{1}{2}$,所以 $\frac{1}{2m}$里分母的 $2$ 的意义是为**梯度下降Gradient Descent**的计算提供方便。

Now we are able to concretely measure the accuracy of our predictor function against the correct results we have so that we can predict new results we don't have.
>现在我们可以具体地测量设计的预测函数的精确度了(?)。由此,我们现在可以预测一些我们之前没有的新结果了





## Gradient Descent
**梯度下降**

So we have our hypothesis function and we have a way of measuring how accurate it is. Now what we need is a way to automatically improve our hypothesis function. That's where gradient descent comes in.
>现在,我们有了自己的 预测函数 和 衡量其准确度如何的方法。接下来我们还需要为我们的预测函数找到自动升级的方法, 这就是我们为什么需要**梯度下降**


Imagine that we graph our hypothesis function based on its fields $\theta_0$ and $\theta_1$ (actually we are graphing the cost function for the combinations of parameters). This can be kind of confusing; we are moving up to a higher level of abstraction. We are not graphing $x$ and $y$ itself, but the guesses of our hypothesis function.
>假设我们基于 $\theta_0$ 和 $\theta_1$ 绘制了我们的**假设函数**（实际上我们为了组合参数绘制了**代价函数**）。可能让人感到困惑的是，我们并不是具体绘制X和y,而是绘制我们的**假设函数**的猜想图：我们现在正拉升至更高一级的抽象角度。

We put $\theta_0$ on the $x$ axis and $\theta_1$ on the $z$ axis, with the cost function on the vertical $y$ axis. The points on our graph will be the result of the **cost function** using our hypothesis with those specific theta parameters.
>我们将 $\theta_0$ 作为 $x$ 轴, $\theta_1$ 作为 $z$ 轴, 代价函数作为 $y$ 轴.在图上得到的点
是我们使用特殊的theta作为参数的假想值得到的**代价函数**
We will know that we have succeeded when our cost function is at the very bottom of the pits in our graph, i.e. when its value is the minimum.
>当我们的代价函数非常接近图像底部,即,取到最小值时,便成功了。

The way we do this is by taking the **derivative** (the line tangent to a function) of our cost function. The slope of the tangent is the derivative at that point and it will give us a direction to move towards. We make steps down that derivative by the parameter $\alpha$, called the learning rate.
>我们使用**导数**(函数的切线)来处理我们的代价函数。该点处的导数是该点切线的斜率，表明了函数的走向。我们进一步将导数用参数 $\alpha$ 表示(?),称为**学习速度**

The gradient descent equation is:
>梯度下降方程：

repeat until convergence:(收敛)
$\theta_{j}:=\theta_{j}-\alpha\frac{\partial}{\partial\theta_{j}}J(\theta_{0},\theta_{1})$


for $j = 0$ and $j = 1$
Intuitively, this could be thought of as:
>直观上，可以认为是

$repeat until convergence:$
$ \theta_{j}:=\theta_{j}-\alpha $[Slope of tangent aka derivative(导数)]

## Gradient Descent for Linear Regression
####线性回归中的梯度递减
When specifically applied to the case of linear regression, a new form of the gradient descent equation can be derived. We can substitute our actual cost function and our actual hypothesis function and modify the equation to (the derivation of the formulas are out of the scope of this course, but a really great one can be [found here](http://math.stackexchange.com/questions/70728/partial-derivative-in-gradient-descent-for-two-variables/189792#189792):

>当被特定地应用在线性回归方程中时,我们使用的是梯度递减的一个衍生公式。修改过的实际的代价函数和实际的假设函数（公式的推导过程超纲了,这里给出[链接](http://math.stackexchange.com/questions/70728/partial-derivative-in-gradient-descent-for-two-variables/189792#189792)）的公式如下：


$repeat until convergence:$ {

$$\theta_{0}:=\theta_{0}-\alpha\frac{1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})$$
$$\theta_{1}:=\theta_{1}-\alpha\frac{1}{m}\sum_{i=1}^{m}((h_{\theta}(x^{(i)})-y^{(i)})x^{(i)})$$

}

where $m$ is the size of the training set,$\theta_0$ a constant that will be changing simultaneously with $\theta_1$ and $x^{(i)},y^{(i)}$ are values of the given training set (data).
>$m$ 是训练集的大小,$\theta_0$ 是随 $\theta_1$ 变化的常量, $x^{(i)},y^{(i)}$ 是给定的训练集的值。

Note that we have separated out the two cases for $\theta_j$ and that for $\theta_1$ we are multiplying $x(i)$ at the end due to the derivative.
>需要注意的是, 我们已经分为了 $\theta_j$ 和 $\theta_1$ 两种情况
最后基于导数乘上 $x(i)$ (?)

The point of all this is that if we start with a guess for our hypothesis and then repeatedly
apply these gradient descent equations, our hypothesis will become more and more accurate.
>所有这一切的目的是,如果我们从我们猜测的假设情况开始,然后反复
应用这些梯度下降法方程,我们的假设将变得越来越准确。

## What's Next
**接下来干啥**

Instead of using linear regression on just one input variable, we'll generalize and expand our concepts so that we can predict data with multiple input variables. Also, we'll solve for $\theta_0$ and $\theta_1$ exactly without needing an iterative function like gradient descent.
>我们将推广和扩大我们的概念,所以我们可以预测数据与多个输入变量, 而不是使用线性回归只有一个输入变量。此外, 我们将会使用类似下降方程这个图多次迭代以外的方法来求 $\theta_0$ 和 $\theta_1$
