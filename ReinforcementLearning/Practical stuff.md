


We define a discount rate called gamma. **It must be between 0 and 1.** Most of the time between **0.99 and 0.95**.



We create a vectorized environment (method for stacking multiple independent environments into a single environment) of 16 environments, this way, **we'll have more diverse experiences during the training.**


[PPO (aka Proximal Policy Optimization) is one of the of the SOTA (state of the art) Deep Reinforcement Learning algorithms that you'll study during this course](https://stable-baselines3.readthedocs.io/en/master/modules/ppo.html#example%5D).



We use MultiLayerPerceptron (MLPPolicy) because the input is a vector, if we had frames as input we would use CnnPolicy

