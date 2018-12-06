[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

---

>> With a million simulated games I got A RMSE= 1.41576516414 and a mean error= 0.001591

>>Given the small size of the mean error and that it is approaching 0 for large n's I'd say this was an unbiased way to estimate. See my code below:


```{python}
def manyGames(n=1000000,lam=2):
    #Get goals for each game
    goals = []
    [goals.append(SimulateGame(lam)) for i in range(n)]
    #compute mean error & RMSE
    print('rmse m', RMSE(goals, lam))
    print('mean error m', MeanError(goals, lam))
    
    
manyGames()

```
---
