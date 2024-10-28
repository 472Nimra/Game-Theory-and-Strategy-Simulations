The provided Python code analyzes the classic game theory scenario known as the **Prisoner's Dilemma** using the `nashpy` library, which specializes in Nash equilibrium calculations. Below is a detailed breakdown of the code, including an explanation of the game setup, payoff matrices, and plotting of the payoff distributions for each player.

### Libraries Used
1. **nashpy**: A library specifically designed for calculating Nash equilibria in game theory.
2. **NumPy** (`import numpy as np`): Used for numerical operations and array manipulation.
3. **Matplotlib** (`import matplotlib.pyplot as plt`): Used for plotting graphs and visualizations.

### Installing the Nashpy Library
```python
pip install nashpy
```
- This command installs the `nashpy` library, which is necessary for handling the Nash equilibrium calculations.

### Payoff Matrices Definition
```python
# Define the payoff matrices for the Prisoner's Dilemma
# Player 1's payoffs
A = np.array([[1, 0],    # Player 1's payoff when Player 2 cooperates
              [3, 2]])   # Player 1's payoff when Player 2 defects

# Player 2's payoffs
B = np.array([[1, 3],    # Player 2's payoff when Player 1 cooperates
              [0, 2]])   # Player 2's payoff when Player 1 defects
```
- The **payoff matrices** `A` and `B` represent the payoffs for Player 1 and Player 2, respectively.
- The first index in matrix `A` and `B` corresponds to Player 1’s choices (cooperate or defect), while the second index corresponds to Player 2’s choices:
  - For Player 1:
    - If Player 2 cooperates, Player 1 receives `1` for cooperating and `0` for defecting.
    - If Player 2 defects, Player 1 receives `3` for cooperating and `2` for defecting.
  - For Player 2:
    - If Player 1 cooperates, Player 2 receives `1` for cooperating and `3` for defecting.
    - If Player 1 defects, Player 2 receives `0` for cooperating and `2` for defecting.

### Creating the Game Instance
```python
# Create a Nashpy Game
prisoners_dilemma = nash.Game(A, B)
```
- A `Game` object representing the Prisoner's Dilemma is created using the defined payoff matrices.

### Calculating Nash Equilibria
```python
# Calculate Nash equilibria
equilibria = prisoners_dilemma.support_enumeration()

print("Nash Equilibria:")
for eq in equilibria:
    print(eq)
```
- The `support_enumeration()` method computes the Nash equilibria of the game.
- Nash equilibria are strategy profiles where no player can benefit by unilaterally changing their strategy.
- The equilibria are printed to the console, displaying the optimal strategies for both players.

### Strategy Distributions for Plotting
```python
# Strategy distributions for plotting
strategies = np.linspace(0, 1, 100)
payoffs_player_1 = []
payoffs_player_2 = []
```
- `strategies` is an array of values between `0` and `1`, representing the probability of Player 1 cooperating.
- `payoffs_player_1` and `payoffs_player_2` are initialized as empty lists to store the corresponding payoffs for Player 1 and Player 2 as Player 1's cooperation probability varies.

### Calculating Payoffs
```python
for p1_strategy in strategies:
    p1_strategy_array = np.array([p1_strategy, 1 - p1_strategy])
    p2_strategy_array = np.array([1 - p1_strategy, p1_strategy])  # Assume symmetric strategies
    payoff_1 = A @ p2_strategy_array
    payoff_2 = B @ p2_strategy_array

    payoffs_player_1.append(payoff_1[0])
    payoffs_player_2.append(payoff_2[0])
```
- The loop iterates over each value in `strategies`, treating it as the probability of Player 1 cooperating.
- `p1_strategy_array` is constructed to represent Player 1’s strategy, while `p2_strategy_array` is derived by assuming symmetric strategies for Player 2.
- The dot product (`@`) of the payoff matrices with the strategy arrays is calculated to derive the payoffs for each player.
- The first element of the resulting arrays (i.e., the payoff when both players cooperate) is appended to their respective lists.

### Plotting the Payoffs
```python
# Plotting the payoffs
plt.figure(figsize=(10, 6))
plt.plot(strategies, payoffs_player_1, label="Player 1 Payoff", color='blue')
plt.plot(strategies, payoffs_player_2, label="Player 2 Payoff", color='orange')
plt.title("Payoff Distribution in Prisoner's Dilemma")
plt.xlabel("Player 1's Cooperation Probability")
plt.ylabel("Payoffs")
plt.axvline(x=0.5, color='grey', linestyle='--', label='Mixed Strategy Equilibrium')
plt.legend()
plt.grid()
plt.show()
```
- A plot is generated showing the payoff distribution for both players based on Player 1's cooperation probability.
- The `plt.plot` method visualizes Player 1’s and Player 2’s payoffs against Player 1's strategy.
- A vertical dashed line is drawn at `x=0.5`, representing the mixed strategy equilibrium, where both players are indifferent to their choices.

### Summary
- This code provides a complete analysis of the Prisoner's Dilemma, illustrating how to compute Nash equilibria and visualize the payoffs for each player's strategies.
- The `nashpy` library simplifies the process of finding equilibria, while NumPy and Matplotlib allow for efficient calculations and clear visualizations.
- Users can easily adjust the payoff matrices to explore different scenarios in game theory, providing a flexible tool for educational and research purposes.
