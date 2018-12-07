[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

*From the instructions: Communicate the problem, how you solved it, and the solution, within each of the following markdown files. (You can include code blocks and images within markdown.)*  

*In Section 9.3, we simulated the null hypothesis by permutation; that is, we treated the observed values as if they represented the entire population, and randomly assigned the members of the population to the two groups.*  

*An alternative is to use the sample to estimate the distribution for the population, then draw a random sample from that distribution. This process is called resampling. There are several ways to implement resampling, but one of the simplest is to draw a sample with replacement from the observed values, as in Section 9.10.*  

*Write a class named DiffMeansResample that inherits from DiffMeansPermute and overrides RunModel to implement resampling, rather than permutation.*  

*Use this model to test the differences in pregnancy length and birth weight. How much does the model affect the results?*  

## Answer

>>This question asks us to try two methods to create a null hypothesis. In the chapter they explained the permutation method. Now they want us to try a resampling method that estimates the distribution for the population then draws a random sample from it. We're then asked to write a class that does this new resampling method and describe how much it does or doesn't affect the results to test the difference in pregnancy length and birth weight. 

>> The first method I tried didn't get the right answer when I checked the solution. I ended up taking the author's method for the DiffMeansResample class which used np.random.choice(self.pool,self.n,replace=True) to resample. My initial approach was to estimate a distribution of the population from the sample, then get its mean and stndard deviation all in the RunModel method of the class. That wasn't giving me the result I wanted so I looked at the solution to see how the author resampled. The author used the short code above twice which after much reading I understand first uses self.pool to call np.hstack and put the 1st and other data back together taking in order each element then combining them. Then it creates a random sample of the combined data using np.random.choice where it takes the pool of data as all of the options to randomly pick from and picks n.self which is really the length of group1 or the first child data. 

>> The rest I did get. I created a quick function to get pvals depending on the test used then ran the prg legnth pval with both methods and the birth weight pval with both methods.

>>See results below. Not much difference between resampling vs. permute.

preglength  
diff means resample preglength  
p-value = 0.166  
diff means permute preglength  
p-value = 0.143  
actual = 0.0780372667775  

Birth weight  
diff means resample preglength  
p-value = 0.0  
diff means permute preglength  
p-value = 0.0  
actual = nan  

>> code:
```python

class DiffMeansResample(DiffMeansPermute):
    def RunModel(self):
        group1 = np.random.choice(self.pool, self.n, replace=True)
        group2 = np.random.choice(self.pool, self.m, replace=True)
        return group1, group2

import first
live, firsts, others = first.MakeFrames()

def getpval(data_var,class_type):
    data = firsts[data_var].values, others[data_var].values
    if class_type == 'DiffMeansResample':
        ht = DiffMeansResample(data)
    if class_type == 'DiffMeansPermute':
        ht = DiffMeansPermute(data)
    pvalue = ht.PValue()
    actual = ht.actual
    return pvalue, actual

a = 'DiffMeansResample'
b = 'DiffMeansPermute'
#print (getpval('totalwgt_lb',a),getpval('totalwgt_lb',b))
#print (getpval('prglngth',a),getpval('prglngth',b))

print('\npreglength')
print('diff means resample preglength')
print('p-value =', getpval('prglngth',a)[0])
print('diff means permute preglength')
print('p-value =', getpval('prglngth',b)[0])
print('actual =', getpval('prglngth',a)[1])

print('\nBirth weight')
print('diff means resample preglength')
print('p-value =', getpval('totalwgt_lb',a)[0])
print('diff means permute preglength')
print('p-value =', getpval('totalwgt_lb',b)[0])
print('actual =', getpval('totalwgt_lb',a)[1])
```
