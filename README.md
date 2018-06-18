# Multi Armed Bandit

## Multi Armed Bandit Scenario

You go to the casino and you have a choice between many slot machines. The reason it is called the multi-armed bandit is because 
each slot machine has a lever which you can pull and ultimately you are being robbed of your money. The win rate and distribution of 
each slot machine is unknown. We need to maximise our winnings by pulling the slot machine with the highest win rate. However, 
we don't know the win rate and the only way to find out is to play lots of machines. The dilemma in short is a trade off between exploring
i.e. collecting data versus exploting i.e. using the best slot machine. Playing the machine we think is the best at that given time could be the same as playing a suboptimal bandit. 

### Solution 1: Epsilon-Greedy

The first solution is known as the epsilon-greedy strategy. How it works? - we use a value called epsilon which is a small number
represented as a probability. This allows us to explore as every arm has a chance to be updated. 

Problem: in the Long-run we may continue to explore sub-optimal arms when we don't need to. 

### Solution 2: Optimistic Values

