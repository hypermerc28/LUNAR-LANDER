# Lunar Lander Hyperparameter Experiment

This repository contains a Jupyter Notebook that demonstrates an experiment with hyperparameters for training a reinforcement learning agent using the Proximal Policy Optimization (PPO) algorithm to solve the Lunar Lander environment from the OpenAI Gym.


## Overview

The notebook explores various hyperparameters and evaluates their impact on the performance of the PPO agent in the Lunar Lander environment. The goal is to find the optimal set of hyperparameters that maximize the agent's performance.

## Contents

- **Setup and Dependencies**: Import necessary libraries and set up the environment.
- **Environment Initialization**: Initialize the Lunar Lander environment with appropriate settings.
- **Model Training**: Train the PPO agent with different sets of hyperparameters.
- **Evaluation**: Evaluate the trained agent's performance using the `evaluate_policy` method.
- **Visualization**: Render and save GIFs of the agent's performance in the environment.

## Key Components

1. **Libraries Used**:
    - `gymnasium`: For the Lunar Lander environment.
    - `stable_baselines3`: For the PPO algorithm.
    - `imageio` and `numpy`: For rendering and saving GIFs.

2. **Hyperparameter Tuning**:
    - Various hyperparameters such as learning rate, clip range, and entropy coefficient are explored to observe their effects on the agent's performance.

3. **Training Process**:
    - The PPO agent is trained over multiple iterations, and performance metrics such as mean reward and standard deviation of rewards are recorded.

4. **Evaluation and Visualization**:
    - The trained agent is evaluated over multiple episodes to obtain the mean and standard deviation of rewards.
    - Episodes are recorded and saved as GIFs to visually inspect the agent's behavior.

## Results

The notebook provides a detailed analysis of the agent's performance with different hyperparameters, including:

- Training metrics such as loss, policy gradient loss, value loss, and explained variance.
- Evaluation metrics such as mean reward and standard deviation of rewards.
- Visualizations of the agent's performance, saved as GIFs.


## Conclusion

This experiment demonstrates the importance of hyperparameter tuning in training reinforcement learning agents. By systematically varying the hyperparameters, we can achieve significant improvements in the agent's performance. The results and visualizations provided in this notebook serve as a valuable resource for understanding the impact of different hyperparameters on the PPO algorithm.

![Training Performance](https://i.imgur.com/f0rPEpQ.png)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

