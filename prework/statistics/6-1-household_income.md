[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

*From the instructions: Communicate the problem, how you solved it, and the solution, within each of the following markdown files. (You can include code blocks and images within markdown.)*

*The Current Population Survey (CPS) is a joint effort of the Bureau of Labor Statistics and the Census Bureau to study income and related variables. Data collected in 2013 is available from http://www.census.gov/hhes/www/cpstables/032013/hhinc/toc.htm. I downloaded hinc06.xls, which is an Excel spreadsheet with information about household income, and converted it to hinc06.csv, a CSV file you will find in the repository for this book. You will also find hinc2.py, which reads this file and transforms the data.*  

*The dataset is in the form of a series of income ranges and the number of respondents who fell in each range. The lowest range includes respondents who reported annual household income “Under $5000.” The highest range includes respondents who made “$250,000 or more.”*  

*To estimate mean and other statistics from these data, we have to make some assumptions about the lower and upper bounds, and how the values are distributed in each range. hinc2.py provides InterpolateSample, which shows one way to model this data. It takes a DataFrame with a column, income, that contains the upper bound of each range, and freq, which contains the number of respondents in each frame.*  

*It also takes log_upper, which is an assumed upper bound on the highest range, expressed in log10 dollars. The default value, log_upper=6.0 represents the assumption that the largest income among the respondents is 106, or one million dollars.*  

*InterpolateSample generates a pseudo-sample; that is, a sample of household incomes that yields the same number of respondents in each range as the actual data. It assumes that incomes in each range are equally spaced on a log10 scale.*  

*Compute the median, mean, skewness and Pearson’s skewness of the resulting sample. What fraction of households reports a taxable income below the mean? How do the results depend on the assumed upper bound?*  

## Answer

>> This question is basically asking us to find a few summary statisitcs of generated sample from a real sample of data. The generated sample is made using a method the author implemented in Python that matches frequencies of responses within ranges to the original data set. For example, the original dataset may have 10 people who make under $5k dollars. The generated sample will also have 10 people in that same range. The summary statistics we investigate aare median, mean, skewness and Pearson's skewness.  

>> I used the author's method to generate data, converted it from a log scale to earnings, created a CDF of it and found the summary stats for the CDF.

>> The mean is 74278.7075312. The median is 51226.4544789. The skew is 4.94992024443. The Pearson skew is 0.736125801914. 0.660005879567 of households report a taxable income below the mean.

>> One big takeaway is that only looking up to 1 million dollars as the data does is probably not a great way to investigate this type of data.  

>> See my code below:

```python
import hinc
income_df = hinc.ReadData()
log_sample = InterpolateSample(income_df, log_upper=6.0)
sample = np.power(10, log_sample)
cdf = thinkstats2.Cdf(sample)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Household income ($)',
               ylabel='CDF')
ansmu = Mean(sample)
ansmedian=Median(sample)
print('The mean is %s. The median is %s.'%(ansmu,ansmedian))
ansSkew = Skewness(sample)
ansPSkew = PearsonMedianSkewness(sample)
print('The skew is %s. The Pearson skew is %s.'%(ansSkew,ansPSkew))
ansf =cdf.Prob(Mean(sample))
print ('%s of households report a taxable income below the mean.'%(ansf))
```


