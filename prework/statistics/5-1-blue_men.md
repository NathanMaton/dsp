[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

*From the instructions: Communicate the problem, how you solved it, and the solution, within each of the following markdown files. (You can include code blocks and images within markdown.)*  

*Exercise 1   In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.*  

*In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.*  

## Answer

>> The question asks us about the percentage of the U.S. male population that fits into the height range to be part of the Blue Man Group using the BRFSS sample dataset.  

>> I used scipy.stats.norm to create a normal distribution based on the BRFSS data. The mean for heights is 178 cms and the std for men is 7.7 cm. If you create a dataset with those parameters then convert the Blue Man Group (BMG) heights into cms you can then use them as a high and low filter in your CDF getting the CDF value of each and then subtracting the larger "top" height CDF value from the smaller one.  

>> The answer I got was 0.34274683763147457, or roughly 1/3rd of the people in the BRFSS data. 

>> See my python code below:

```python
import scipy.stats
mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)
#convert filters into cms
param1 = ((5*12)+10)* 2.54
param2 = ((6*12)+1)* 2.54
#calculate cdf
bottom = dist.cdf(param1)
top = dist.cdf(param2)
#get difference
ans = top-bottom
ans
``` 
