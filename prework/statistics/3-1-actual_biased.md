[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

*From the instructions: Communicate the problem, how you solved it, and the solution, within each of the following markdown files. (You can include code blocks and images within markdown.)*  

*Problem 1: Exercise: Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.*

*Use the NSFG respondent variable numkdhh to construct the actual distribution for the number of children under 18 in the respondents' households.*  

*Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.*  

*Plot the actual and biased distributions, and compute their means.*  

>>The problem here is to demonstrate how surveys can be biased using the NSFG data. I solved this by creating a dictionary of actual children under 18 in respondent's household. Then I used Allen's BiasPmf function and plotted the result.   

## Plot:

![Plot of actual number of kids in household vs. if kids were surveyed](plotfor31.png)


## Computed means:
Actual mean 1.024  
Mean if kids were surveyed 2.404  

>> The results would be very biased if we asked kids, effectively demonstrating the point of how bias in surveys can work.  

>> If you're interested here's the code I used:
```python
resp['numkdhh'].value_counts().sort_index()
d = { 0:3563,1:1636,2:1500,3:666,4:196,5:82 }

pmf = thinkstats2.Pmf(d, label='actual')
biased_pmf = BiasPmf(pmf, label='if kids were surveyed')
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased_pmf])
thinkplot.Config(xlabel='Class size', ylabel='PMF')
``` 
