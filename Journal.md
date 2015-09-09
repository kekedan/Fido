# Fido Research Journal

### Progress made over the summer
#### Software - Michael Truell
We began by familiarizing ourselves with the scientific literature on neural networks and their uses. I began with a fabulous tutorial on using neural networks paired with a genetic algorithm to solve tasks (http://www.ai-junkie.com/ann/evolved/nnt1.html). Then general implementations of a neural network and a genetic algorithm were written. To test these two pieces of software, neural networks were taught to play tic tac toe by playing against one another and by being subject to our genetic algorithm. Once this was done, I familiarized myself with backpropagation, an algorith widely used to train neural networks given a set of training data, by reading a number of introductory papers on the subject. After this, an implentation of backpropagation was written and added to our code base. It was tested by teaching a neural network to perform some simple linear regression. To further test the power of our software, we used our genetic algorithm implemenatation to teach neural networks to play Halite, a game for AIs made by our friend and classmate Benjamin Spector (10th grade), and used our backpropagation implementation to teach neural networks how to perform linear and nonlinear regression.

We then turned our sights on the topic of our project, reinforcement learning. We implemented the popular algorithm Q-learn, for teaching function approximators (a feedforward neural network is just a function approximator) descrete actions. We added in some non-random search heuristics, so that our NNs could learn in large state and action spaces. We tested our implementations on simple tasks, like turning on an LED when prompted with the proper stimuli (like a flash of light), using a simulator that we built. However, though our q-learning implementation can handle continous state spaces, our neural networks will have to carry out continuous actions (like the setting of motor values), and so it was neccessary to extend our Q Learning implementation into one that could handle continuous action spaces. We turned to the use of a wire-fitted least squares interpolator couple with a neural network as described in Gasket et al. (http://users.cecs.anu.edu.au/~rsl/rsl_papers/99ai.kambara.pdf). We are currently testing and modifying this algorithm so that it converges on the correct method for completing a task with less human feedback

#### Hardware - Joshua Gruenstein

### September 7, 2015
#### Michael Truell
A WireFitRobot class was created that connected our of Wire Fit Q Learn implementation to our simulator. This was taught a number of simple tasks, such as to drive as fast as possible and to drive straight. Learning to drive as fast as possible was defined as choosing a speed above 95% for five iterations of feedback in a row and learning to drive straight was classified as having a difference of motor values of less than 0.05 for five iterations of feedack in a row. However, the number of inputs required by a human subject before the robot learned succesfully is quite high. For a WireFitQLearn object with 3 wires, it was on the order of 50 to learn drive straight and around 15 to drive fast. In contrast, for our discrete Q-Learn implementation it took less than 10 feedback iterations for it to learn to only turn on an LED when triggered by the proper stimulus.

This can surely be fixed with modifications to the present Wire Fit Q-learn implementation. Right now, a reward is tagged to an action, which is used to update the Q-value (or long term reward) of the action. Stocastic gradient descent is used to modify the control points outputed by the neural network, so that the control points produce an interpolator function that accurately outputs the reward.

The WireFitQLearn object can be modified for the better by instead changing the control points each reward iteration so that they have produce a function that not just accurately outputs the reward value given that iterations, but one that also will accurately output reward values values from past iterations when given their respective actions. Reward-action pairs should be devalued based on how old they are by giving them a greater acceptable error value (the distance the output of the function produced from gradient descent is from the correct reward value) as they age.