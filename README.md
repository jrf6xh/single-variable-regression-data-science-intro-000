
# Intro to regression lines

### Learning Objectives

* Understand how regression lines can help us make predictions about data
* Understand how the components of slope and y-intercept determine the output of a regression line 
* Understand how to represent a line as a function

### A not so simple problem

Now we know a bit about plotting data and we have written some functions, like the `trace_values`, `layout`, and `plot`, to help us do so.  You can [view them here](https://github.com/learn-co-curriculum/single-variable-regression/blob/master/lib/graph.py).

### The benefit of a buck

Imagine we are hired as a consultant for a movie executive.  The movie executive receives a budget proposal, and wants to know how much money the movie might make.  We can help him by building a model of the relationship between the money spent on a movie and money made. 

### Representing linear regression graphically

To predict movie revenue based on a budget, let's draw a single straight line that represents the relationship between how much a movie costs and how much it makes.  

> Eventually, we will want to **train** this model to match up against an actual data, but for now let's just draw a line to see how it can make estimates.


```python
from lib.graph import trace_values, plot, layout

regression_trace = trace_values([0, 150], [0, 450], mode = 'lines', name = 'estimated revenue')
movie_layout = layout(options = {'title': 'Movie Spending and Revenue (in millions)'})
plot([regression_trace], movie_layout)
```

By using a line, we can see how much money is earned for any point on this line.  All we need to do is look at a given $x$ value, and find the corresponding $y$ value at that point on the line. 

* Spend 60 million, and expect to bring in about 180 million.  
* Spend 20 million, and expect to bring in 60 million.  

This approach of modeling a linear relationship (that is a drawing a straight line) between an input and an output is called **linear regression**.  We call the input our **explanatory variable**, and the output the **dependent variable**.  So here, we are saying budget *explains* our dependent variable, revenue.

### Representing linear regression with functions

Instead of only representing this line visually, we also would like to represent this line with a function. That way, instead of having to **see** how an $x$ value points to a $y$ value along our line, we simply could punch this input into our function to calculate the proper output.  

#### A wrong guess
Let's take an initial (wrong) guess at turning this line into a function.  

**First**, we represent the line as a mathematical formula.

$y = x$

**Then**, we turn this formula into a function:


```python
def y(x):
    return x

y(0)
```


```python
y(10000000)
```

This is pretty nice.  We just wrote a function that automatically calculates the expected revenue given a certain movie budget.  This function says that for every value of $x$ that we input to the function, we get back an equal value $y$.  So according to the function, if the movie has a budget of $30$ million, it will earn $30$ million. 

#### A better guess: Matching lines to functions
Take a look at the line that we drew.  Our line says something different.  The line says that spending 30 million brings predicted earnings of 90 million.  We need to change our function so that it matches our line.  In fact, we need a consistent way to turn lines into functions, and vice versa.  Let's get to it.

**We start** by turning our line into a chart below.  It shows how our line relates x-values and y-values, or our budgets and revenues.

| X (budget)       | Y (revenue)           | 
| ------------- |:-------------:| 
| 0      |0 | 
| 30 million      |90 million | 
| 60 million      |180 million | 

**Next**, we need an equation that allows us to match this data.
* input 0 and get back 0
* input 30 million and get back 90 million
* and input 60 million and get back 180 million?  

What equation is that?  Well it's $y = 3x$.  Take a look to see for yourself.

* 0 * 3 = 0
* 30 million * 3 = 90 million
* 60 million * 3 = 180 million 

Let's see it in the code.  This is what it looks like:


```python
def y(x):
    return 3*x
```


```python
y(30000000)
```


```python
y(0)
```

Progress! We multiplied each $x$ value by 3 so that our function's outputs correspond to the $y$ values appearing along our graphed line.

### The Slope Variable 

By multiplying $x$ by 3, we just altered the **slope variable**.  The slope variable changes the inclination of the line in our graph.  Slope generally is represented by $m$ like so:

$y = mx$ 

Let's make sure we understand what all of our variables stand for.  Here they are: 

* $y$: the output value returned by the function, also called the **response variable**, as it responds to values of $x$
* $x$: the input variable, also called the **explanatory variable**, as it explains the value of $y$
* $m$: the **slope variable**, determines how vertical or horizontal the line will appear

Let's adapt these terms to our movie example.  The $y$ value is the revenue earned from the movie, which we say is in *response* to our budget.  The *explanatory variable* of our budget, $x$, represents our budget, and the $m$ corresponds to our value of 3, which describes how much money is earned for each dollar spent.  Therefore, with an $m$ of 3, our line says to expect to earn 3 dollars for each dollar spent making the movie.  Likewise, an $m$ of 2 suggests we earn 2 dollars for every dollar we spend.

> A higher value of $m$ means a steeper line.  It also means that we expect more money earned per dollar spent on our movies.  Imagine the line pivoting to a steeper tilt as we guess a higher amount of money earned per dollar spent.  

### The y-intercept

There is one more thing that we need to learn in order to describe every straight line in a two-dimensional world.  That is the **y-intercept**.

> * The **y-intercept** is the $y$ value of the line where it intersects the y-axis.  
> * Or, put another way, the y-intercept is the value of $y$ when $x$ equals zero.  

Let's add a trace with a higher y-intercept than our initial line to the movie plot.  


```python
regression_trace_increased = trace_values([0, 150], [50, 500], mode = 'lines', name = 'increased est. revenue')
plot([regression_trace_increased, regression_trace], movie_layout)
```

What is the y-intercept of the original estimated revenue line?  Well, it's the value of $y$ when that line crosses the y-axis.  That value is zero.  Our second line is parallel to the first but is shifted higher so that the y-intercept increases up to 50 million.  Here, for every value of $x$, the corresponding value of $y$ is higher by 50 million.  

* Our formula is no longer $y = 3x$.  
* It is $y = 3 x + 50,000,000$. 

In addition to determining the y-intercept from a line on a graph, we can also see the y-intercept by looking at a chart of points.  

> In the chart below, we know that the y-intercept is 50 million because its corresponding $x$ value is zero. 

| X        | Y           | 
| ------------- |:-------------:| 
| 0      |50 million | 
| 40 million      |170 million | 
| 60 million      |230 million | 

The y-intercept of a line usually is represented by *b*.  Now we have all of the information needed to describe any straight line using the formula below:  

$$y = mx + b $$

Once more, in this formula: 
* $m$ is our slope of the line, and
* $b$ is the value of $y$ when $x$ equals zero.  

So thinking about it visually, increasing $m$ makes the line steeper, and increasing $b$ pushes the line higher.   

In the context of our movies, we said that the the line with values of $m$ = 3 and $b$ = 50 million describes our line, giving us:

$y = 3x + 50,000,000 $.

Let's translate this into a function.  For any input of $x$ our function returns the value of $y$ along that line.  


```python
def y(x):
    return 3*x + 50000000
```


```python
y(30000000)
```


```python
y(60000000)
```

### Summary

In this section, we saw how to estimate the relationship between an input variable and an output value.  We did so by drawing a straight line representing the relationship between a movie's budget and it's revenue.  We saw the output for a given input simply by looking at the y-value of the line at that input point of $x$.  

We then learned how to represent a line as a mathematical formula, and ultimately a function.  We describe lines through the formula $y = mx + b $, with $m$ representing the slope of the line, and $b$ representing the value of $y$ when $x$ equals zero.  The $b$ variable shifts the line up or down while the $m$ variable tilts the line forwards or backwards.  Translating this formula into a function, we can write a function that returns an expected value of $y$ for an input value of $x$.
