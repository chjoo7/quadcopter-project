# Project: Train a Quadcopter How to Fly
- Design an agent to fly a quadcopter, and then train it using a _reinforcement learning_ algorithm of your choice! 
Try to apply the techniques you have learnt, but also feel free to come up with innovative ideas and test them.

## Instruction
Take a look at the files in the directory to better understand the structure of the project. 
    -task.py: Define your task (environment) in this file.
    -agents/: Folder containing reinforcement learning agents.
    -policy_search.py: A sample agent has been provided here.
    -agent.py: Develop your agent here.
    -physics_sim.py: This file contains the simulator for the quadcopter. **DO NOT MODIFY THIS FILE**.
  For this project, you will define your own task in task.py. Although we have provided a example task to get you started, you are encouraged to change it. Later in this notebook, you will learn more about how to amend this file.
You will also design a reinforcement learning agent in agent.py to complete your chosen task. 
You are welcome to create any additional files to help you to organize your code. For instance, you may find it useful to define a model.py file defining any needed neural network architectures.

# Installation

_git clone https://github.com/chjoo7/quadcopter-project.git_


## Controlling the Quadcopter
Jupyter notebook provides a sample agent in the code cell to show you how to use the sim to control the quadcopter. This agent is even simpler than the sample agent that you'll examine (in agents/policy_search.py) later in this notebook!
The agent controls the quadcopter by setting the revolutions per second on each of its four rotors. The provided agent in the Basic_Agent class below always selects a random action for each of the four rotors. These four speeds are returned by the act method as a list of four floating-point numbers. 
For this project, the agent that you will implement in agents/agent.py will have a far more intelligent method for selecting actions!

## The Task
A sample task has been provided for you in task.py. Open this file in a new window now. 
The __init__() method is used to initialize several variables that are needed to specify the task. 
 -The simulator is initialized as an instance of the PhysicsSim class (from physics_sim.py). 
 -Inspired by the methodology in the original DDPG paper, we make use of action repeats. For each timestep of the agent, we step the   simulation action_repeats timesteps. If you are not familiar with action repeats, please read the Results section in the DDPG paper.
 -We set the number of elements in the state vector. For the sample task, we only work with the 6-dimensional pose information. To set the size of the state (state_size), we must take action repeats into account. 
 -The environment will always have a 4-dimensional action space, with one entry for each rotor (action_size=4). You can set the minimum (action_low) and maximum (action_high) values of each entry here.
 -The sample task in this provided file is for the agent to reach a target position. We specify that target position as a variable.
 
The reset() method resets the simulator. The agent should call this method every time the episode ends. You can see an example of this in the code cell below.

The step() method is perhaps the most important. It accepts the agent's choice of action rotor_speeds, which is used to prepare the next state to pass on to the agent. Then, the reward is computed from get_reward(). The episode is considered done if the time limit has been exceeded, or the quadcopter has travelled outside of the bounds of the simulation.


## The Agent
The sample agent given in agents/policy_search.py uses a very simplistic linear policy to directly compute the action vector as a dot product of the state vector and a matrix of weights. Then, it randomly perturbs the parameters by adding some Gaussian noise, to produce a different policy. Based on the average reward obtained in each episode (score), it keeps track of the best set of parameters found so far, how the score is changing, and accordingly tweaks a scaling factor to widen or tighten the noise.

## Define the Task, Design the Agent, and Train Your Agent!
Amend task.py to specify a task of your choosing. If you're unsure what kind of task to specify, you may like to teach your quadcopter to takeoff, hover in place, land softly, or reach a target pose. 

After specifying your task, use the sample agent in agents/policy_search.py as a template to define your own agent in agents/agent.py. You can borrow whatever you need from the sample agent, including ideas on how you might modularize your code (using helper methods like act(), learn(), reset_episode(), etc.).

Note that it is highly unlikely that the first agent and task that you specify will learn well. You will likely have to tweak various hyperparameters and the reward function for your task until you arrive at reasonably good behavior.
As you develop your agent, it's important to keep an eye on how it's performing. Use the code above as inspiration to build in a mechanism to log/save the total rewards obtained in each episode to file. If the episode rewards are gradually increasing, this is an indication that your agent is learning.