[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

*From the instructions: Communicate the problem, how you solved it, and the solution, within each of the following markdown files. (You can include code blocks and images within markdown.)*  

*Problem from the book: Exercise 4   Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length?*  

>>I solved this by using Cohen's D. There's a good implementation of it in the chapter 2 exercises iPython notebook. I used that and then split the live babies into 2 groups, 1 with first babies and 1 with the others. Then I ran the implementation of Cohen's D on it. 

```python
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d


firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

CohenEffectSize(firsts.totalwgt_lb,others.totalwgt_lb)
```

>>The answer was: -0.088672927072602006 and I believe the units are standard deviations. This is pretty small, and we haven't tested it for statistical significance. In either case, not much to report, first babies may be slightly lighter than others according to Cohen's D.  
