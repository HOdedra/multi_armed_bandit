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


### Acknowledgments

* thelazyprogrammer
