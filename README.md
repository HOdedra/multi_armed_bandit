# Multi Armed Bandit

![Alt Text](https://conversionxl.com/wp-content/uploads/2015/09/gambling-machine-4926_640-1.jpg)

## Multi Armed Bandit Scenario

You go to the casino and you have a choice between many slot machines. The reason it is called the multi-armed bandit is because 
each slot machine has a lever which you can pull and ultimately you are being robbed of your money. The win rate and distribution of 
each slot machine is unknown. We need to maximise our winnings by pulling the slot machine with the highest win rate. However, 
we don't know the win rate and the only way to find out is to play lots of machines. The dilemma in short is a trade off between exploring
i.e. collecting data versus exploting i.e. using the best slot machine. Playing the machine we think is the best at that given time could be the same as playing a sub-optimal bandit. 

## Solution 1: Epsilon-Greedy

The first solution is known as the epsilon-greedy strategy. How it works? - we use a value called epsilon which is a small number
represented as a probability. This allows us to explore as every arm has a chance to be updated. 
The best lever is selected for a proportion 1-epsilon  of the trials, and a lever is selected at random (with uniform probability) for a proportion epsilon . A typical parameter value might be epsilon =0.1, but this can vary widely depending on circumstances and predilections.

Problem: in the Long-run we may continue to explore sub-optimal arms when we don't need to. 

[Solution 1](experimenting_with_epsilon_bandit.py)

![Alt Text](http://g.recordit.co/WYAPWP43kd.gif) ![Alt Text](http://g.recordit.co/clAOImEZhu.gif)

### Explanation of Results 

The algorithm works by assigning three different means to three different bandits. In addition we experiment with three different epsilon values (10%, 5%, 1%):

* Bandit 1 - mean = 1.0

* Bandit 2 - mean = 2.0

* Bandit 3 - mean = 3.0

Ideally, we would like to keep pulling bandit 3 as this has the highest mean reward of 3.0. As you can see from the results the cumulative average converges to a mean of 3.0 as we would like it to. Our algorithm is learning, it is getting reinforced by previous good plays!


## Solution 2: Optimistic Values

In this solution we start with an assertion that the true mean is below 10. We pick a "high ceiling" for an initial estimate of the bandit mean. This is known as optimistic as we are essentially saying this mean is too good to be true and after each update we are getting closer to the true value. The mean should start to decrease. 

Exploitation happens after we collect many samples and we are start to approach our true mean values. 
Exploration happens when a mean of a bandit is too high. This forces us to explore that bandit. The mean will be higher than everything else. 

We deploy only a greedy strategy here! 

[Solution 2](optimistic_initial_values.py)

![Alt Text](http://g.recordit.co/qjDWbn6DBr.gif) ![Alt Text](http://g.recordit.co/tUsbNRVHaB.gif)

The Optimistic algorithm outperforms the epsilon-greedy solution


## Solution 3: Upper-Confidence Bound (UCB)

The Multi-armed bandit problem can also be applied to advertisement and I will be drawing upon a fictional case study to see both its applications and enable us to understand more specifically the UCB algorithm. 

If we are to imagine we are running a campaign to market a product and we would like to discover and predict which is the better advert we would need to know the underlying distribution. By this I mean we must know which advert would be clicked the most therefore having the highest 'Click through rate'. One strategy is an AB test which is pure exploring but not exploitation however we would like to exploit whilst exploring. 

Intuition:

1. D ARMS = each arm is an advert
2. Each time a user connects to the webpage that makes a round
3. At each round n, we choose one ad to display to the user
4. At each round n, ad i gives reward ri(n) which is either 0,1. Either 1 if advert is clicked or 0 otherwise. 
5. Maximise the total reward we get over many rounds

Important: We don't know the distributions of each campaign but we need to maximise the return as the campaign is ongoing. 

What the algorithm does:
We will firstly assume a starting point and assume each advert has the same return. The formula creates a confidence bound which includes the actual expected return. For the first couple of rounds we will run it just as an experiment. We only care about the upper bound within this confidence interval and hence the name Upper Confidnce Bound Algorithm. The algorithm then pulls a lever on a random machine and we see whether the user clicked on it. If it wasn't  clicked the observed average will fall. Due to the Law of Large numbers this observed average should converge to the expected average. As we continue to run through this algorithm the confidence interval becomes smaller because we have an initial observation making us slightly more confident. After completing this we then find the next advert with the highest confidence bound. This impacts the average. We keep doing this until we find the highest confidence bound. Also by exploring options we are decreasing the confidence bound. 

DATASET - dataset containing 10,000 users and what they would click if shown an advert. This is like a 'God File'. A scenario where we are all knowing. 

The code is linked below of which I have included a random strategy and the UCB algorithm. 

[Random & UCB_CTR](ucb_algo_ctr.py)




### Acknowledgments

* thelazyprogrammer
