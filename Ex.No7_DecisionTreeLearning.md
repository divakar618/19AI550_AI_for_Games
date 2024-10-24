# Ex.No: 7 Implementation of Decision Tree Learning 
## DATE:
## REGISTER NUMBER : 212222240026
# AIM:
Design a decision tree for following data. 
1 Healthy, In Cover, With Ammo -> Attack
2.Hurt, In Cover, With Ammo -> Attack
3.Healthy, In Cover, Empty -> Defend
4.Hurt, In Cover, Empty -> Defend
5.Hurt, Exposed, With Ammo -> Defend
# Algorithm:
1. Start the program
2. import the necessary packages 
3. Design a training data and test data 
4. Create a decision tree classifier model
5. Output the predictions 
6. Visualize the decision tree 
# Program:

```python
# Define a large negative and positive value to represent infinity
INF = float('inf')

# Alpha-Beta Pruning function
def alpha_beta_pruning(depth, node_index, maximizing_player, values, alpha, beta):
    # Base case: leaf node is reached
    if depth == 3:
        return values[node_index]
    
    if maximizing_player:
        max_eval = -INF
        # Recur for the two children of the current node
        for i in range(2):
            eval = alpha_beta_pruning(depth + 1, node_index * 2 + i, False, values, alpha, beta)
            max_eval = max(max_eval, eval)
            alpha = max(alpha, eval)
            
            # Prune the branch
            if beta <= alpha:
                break
        return max_eval
    else:
        min_eval = INF
        # Recur for the two children of the current node
        for i in range(2):
            eval = alpha_beta_pruning(depth + 1, node_index * 2 + i, True, values, alpha, beta)
            min_eval = min(min_eval, eval)
            beta = min(beta, eval)
            
            # Prune the branch
            if beta <= alpha:
                break
        return min_eval

# Driver code
if _name_ == "_main_":
    # This is the terminal/leaf node values of the game tree
    values = [3, 5, 6, 9, 1, 2, 0, -1]

    print("Optimal value:", alpha_beta_pruning(0, 0, True, values, -INF, INF))
```


# Output:

![377790164-b4b37ab0-b97e-4bb6-b0eb-4aa1d66a4999](https://github.com/user-attachments/assets/7a694d25-ecb6-465d-9d6d-5de08ea5a42b)



# Result:
Thus the optimum value of max player was found using minimax search.
