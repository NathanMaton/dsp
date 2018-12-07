[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

*From the instructions: Communicate the problem, how you solved it, and the solution, within each of the following markdown files. (You can include code blocks and images within markdown.)*  

*In games like hockey and soccer, the time between goals is roughly exponential. So you could estimate a team’s goal-scoring rate by observing the number of goals they score in a game. This estimation process is a little different from sampling the time between goals, so let’s see how it works.*  

*Write a function that takes a goal-scoring rate, lam, in goals per game, and simulates a game by generating the time between goals until the total time exceeds 1 game, then returns the number of goals scored.*  

*Write another function that simulates many games, stores the estimates of lam, then computes their mean error and RMSE.*  

*Is this way of making an estimate biased? Plot the sampling distribution of the estimates and the 90% confidence interval. What is the standard error? What happens to sampling error for increasing values of lam?*  

## Answer

>> This question is fun. The author suggests a way to model how goal scoring works in games like hockey and soccer, saying the time between goals is roughly exponential. He asks you to create a few functions to test if this hypothesis is accurate. We create a function that returns goals scored based on a goal scoring rate (lambda) and another function that simulates many games and stores estimates of goals and computes their mean error and RMSE. 

>> The questions the author asks at the end are whether this approach is biased, what the standard error and 90% confidence level is and what happens to the sampling error for increasing values of lambda.

>> To approach this I used the function the author already created to simulate goals scored, then created a function to simulmate many games. I ran that function with different values of n.

>> With a million simulated games I got A RMSE= 1.41576516414 and a mean error= 0.001591. With fewer (n = 5 and 100) I got RMSEs of 1.9 and 1.3 respectively. I got mean errors of 1 and -.11 respectively.  

>>Given the small size of the mean error and that it is approaching 0 for large n's I'd say this was an unbiased way to estimate. 

>>When I tried with other lambdas I found the RMSE was higher (2.24 for n=1,000,000 lambda =5), but the mean error was still very low at .0013.

>> See my code below that calculates after n games the RMSE and mean error.

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
