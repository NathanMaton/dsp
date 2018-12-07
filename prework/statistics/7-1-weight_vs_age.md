[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

*From the instructions: Communicate the problem, how you solved it, and the solution, within each of the following markdown files. (You can include code blocks and images within markdown.)*  

*Exercise 1   Using data from the NSFG, make a scatter plot of birth weight versus mother’s age. Plot percentiles of birth weight versus mother’s age. Compute Pearson’s and Spearman’s correlations. How would you characterize the relationship between these variables?*  

## Answer  

>> The question asks us to explore correlations between birth weight and mother's age in a few ways including a scatter plot, a percentiles plot, Pearson's & Spearman's correlation values. Overall, it asks us to characterize the relationships between the values.  

>> To do this I get the data, sort & clean it. Then I use the thinkplot.Scatter method to create a scatter plot. Then I bin the data using np & groupby methods to graph the percentiles plot. I use the Corr & SpearmanCorr methods then to find the correlation values.

>> The data shows a minor correlation that is likely non-linear since the Spearman value is higher than Person's value. You can also see that in the graphs below where the percentiles are not linear.

>> The Pearson correlation is 0.0688339703541. The Spearman rank correlation is 0.0946100410966.

## Scatter plot of birth weight vs. mother's age

![Scatter plot](sp.png)

## Percentile graph of birth weigh vs. mother's age (binned)

![Percentile graph](pg.png)

>> See my code below:

```python
import first

live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])
mA = live['agepreg']
bW = live['totalwgt_lb']

thinkplot.Scatter(mA, bW)
thinkplot.Config(xlabel='Mother\'s age',
                 ylabel='Birth weight',
                 axis=[10,50, 0, 20])

bins = np.arange(10, 48, 3)
indices = np.digitize(live.agepreg, bins)
groups = live.groupby(indices)
mean_age = [group.agepreg.mean() for i, group in groups][1:-1]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups][1:-1]
for percent in [75, 50, 25]:
    weight_percentiles = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(mean_age, weight_percentiles, label=label)
    
thinkplot.Config(xlabel='Mother Age at Birth (binned)',
                 ylabel='Birgh Weight',
                legend=True,
                 axis=[10,50,6,8.5])

print ('The Pearson correlation is ' +str(Corr(mA,bW)))
print ('The Spearman rank correlation is ' +str(SpearmanCorr(mA,bW)))
print ('This shows that there is a minor correlation that is likely non-linear as Spearman is higher. You can also see that in the graphs below where the percentiles are not linear.')
```



