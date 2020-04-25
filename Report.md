[//]: # (Image References)

[image1]: https://github.com/Apunti/RL-Udacity-Collaboration-Competition/master/images/DDPG.png "DDPG"
[image2]: https://github.com/Apunti/RL-Udacity-Collaboration-Competition/master/images/plot.png "Plot"
[image3]: https://github.com/Apunti/RL-Udacity-Collaboration-Competition/master/images/log.png "Log"

# Report

### Learning Algorithm
The algorithm used to solve this environment is an off-policy method called DDPG (Deep Deterministic Policy Gradient) presented in
[this paper](https://arxiv.org/abs/1509.02971). Two handle the two agents, the input is the concatenation of both states (size 48) and the action is of size (4). Taking into account that we then resize the output to a (2,2) matrix to give it to the Unity environment.

Deep Deterministic Policy Gradient (DDPG) is an algorithm which concurrently learns a Q-function and a policy. It uses off-policy data and the Bellman equation to learn the Q-function, and uses the Q-function to learn the policy.

![DDPG][image1]

For further explanation I recommend reading the [spinningup openai website](https://spinningup.openai.com/en/latest/algorithms/ddpg.html).

The architecture for the actor consists of 3 fully connected layers, combined with BatchNormalization, with Relu activation and the output with tanh activation.
in
The architecture for the critic consists of 3 fully connected layers. I applied a BatchNormalization after the first layer, and the actions are inserted in the second. The activation function used is Relu and the output is a linear layer without activation function.

We must remember that the input to the model is the concatenation of the states of both agents, and the output of the actor is of size 4, the first two correspond to the first agent, and the last two correspond to the second agent. In a sense, we consider an agent with two rackets.

The hyperparameters used are:

- ``BUFFER_SIZE = 1e6``
- ``BATCH_SIZE = 128``
- ``GAMMA = 0.99``
- ``TAU = 0.001``
- ``LR_ACTOR = 3e-4``
- ``LR_CRITIC = 3e-4``

### Plot of rewards

![Plot][image2]
![Log][image3]

We can see that the environment is solved around the episode 1800.

### Ideas for Future Works

To improve the current implementation we could use a MADDPG and see its performance. Probably by considering two agents will lead to better results and faster convergence. Moreover, we could try to add prioritized experience replay. For now, the model takes a random sample from the buffer, but by using prioritized experience replay, the model should converge faster.
