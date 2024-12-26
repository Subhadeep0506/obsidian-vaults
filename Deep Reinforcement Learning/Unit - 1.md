# Train your first Deep Reinforcement Learning Agent 🤖

[![Ask a Question](https://img.shields.io/badge/Ask%20a%20question-ffcb4c.svg?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgLTEgMTA0IDEwNiI+PGRlZnM+PHN0eWxlPi5jbHMtMXtmaWxsOiMyMzFmMjA7fS5jbHMtMntmaWxsOiNmZmY5YWU7fS5jbHMtM3tmaWxsOiMwMGFlZWY7fS5jbHMtNHtmaWxsOiMwMGE5NGY7fS5jbHMtNXtmaWxsOiNmMTVkMjI7fS5jbHMtNntmaWxsOiNlMzFiMjM7fTwvc3R5bGU+PC9kZWZzPjx0aXRsZT5EaXNjb3Vyc2VfbG9nbzwvdGl0bGU+PGcgaWQ9IkxheWVyXzIiPjxnIGlkPSJMYXllcl8zIj48cGF0aCBjbGFzcz0iY2xzLTEiIGQ9Ik01MS44NywwQzIzLjcxLDAsMCwyMi44MywwLDUxYzAsLjkxLDAsNTIuODEsMCw1Mi44MWw1MS44Ni0uMDVjMjguMTYsMCw1MS0yMy43MSw1MS01MS44N1M4MCwwLDUxLjg3LDBaIi8+PHBhdGggY2xhc3M9ImNscy0yIiBkPSJNNTIuMzcsMTkuNzRBMzEuNjIsMzEuNjIsMCwwLDAsMjQuNTgsNjYuNDFsLTUuNzIsMTguNEwzOS40LDgwLjE3YTMxLjYxLDMxLjYxLDAsMSwwLDEzLTYwLjQzWiIvPjxwYXRoIGNsYXNzPSJjbHMtMyIgZD0iTTc3LjQ1LDMyLjEyYTMxLjYsMzEuNiwwLDAsMS0zOC4wNSw0OEwxOC44Niw4NC44MmwyMC45MS0yLjQ3QTMxLjYsMzEuNiwwLDAsMCw3Ny40NSwzMi4xMloiLz48cGF0aCBjbGFzcz0iY2xzLTQiIGQ9Ik03MS42MywyNi4yOUEzMS42LDMxLjYsMCwwLDEsMzguOCw3OEwxOC44Niw4NC44MiwzOS40LDgwLjE3QTMxLjYsMzEuNiwwLDAsMCw3MS42MywyNi4yOVoiLz48cGF0aCBjbGFzcz0iY2xzLTUiIGQ9Ik0yNi40Nyw2Ny4xMWEzMS42MSwzMS42MSwwLDAsMSw1MS0zNUEzMS42MSwzMS42MSwwLDAsMCwyNC41OCw2Ni40MWwtNS43MiwxOC40WiIvPjxwYXRoIGNsYXNzPSJjbHMtNiIgZD0iTTI0LjU4LDY2LjQxQTMxLjYxLDMxLjYxLDAsMCwxLDcxLjYzLDI2LjI5YTMxLjYxLDMxLjYxLDAsMCwwLTQ5LDM5LjYzbC0zLjc2LDE4LjlaIi8+PC9nPjwvZz48L3N2Zz4=)](http://hf.co/join/discord)[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/huggingface/deep-rl-class/blob/main/notebooks/unit1/unit1.ipynb)

Now that you’ve studied the bases of Reinforcement Learning, you’re ready to train your first agent and share it with the community through the Hub 🔥: A Lunar Lander agent that will learn to land correctly on the Moon 🌕
# Unit 1: Train your first Deep Reinforcement Learning Agent 🤖
In this notebook, you’ll train your **first Deep Reinforcement Learning agent** a Lunar Lander agent that will learn to **land correctly on the Moon 🌕**. Using [Stable-Baselines3](https://stable-baselines3.readthedocs.io/en/master/) a Deep Reinforcement Learning library, share them with the community, and experiment with different configurations

### The environment 🎮
- [LunarLander-v2](https://gymnasium.farama.org/environments/box2d/lunar_lander/)
### The library used 📚
- [Stable-Baselines3](https://stable-baselines3.readthedocs.io/en/master/)

We’re constantly trying to improve our tutorials, so **if you find some issues in this notebook**, please [open an issue on the Github Repo](https://github.com/huggingface/deep-rl-class/issues).

## Objectives of this notebook 🏆

At the end of the notebook, you will:
- Be able to use **Gymnasium**, the environment library.
- Be able to use **Stable-Baselines3**, the deep reinforcement learning library.
- Be able to **push your trained agent to the Hub** with a nice video replay and an evaluation score 🔥.

Let’s do a small recap on what we learned in the first Unit:

- Reinforcement Learning is a **computational approach to learning from actions**. We build an agent that learns from the environment by **interacting with it through trial and error** and receiving rewards (negative or positive) as feedback.
    
- The goal of any RL agent is to **maximize its expected cumulative reward** (also called expected return) because RL is based on the _reward hypothesis_, which is that all goals can be described as the maximization of an expected cumulative reward.
    
- The RL process is a **loop that outputs a sequence of state, action, reward, and next state**.
    
- To calculate the expected cumulative reward (expected return), **we discount the rewards**: the rewards that come sooner (at the beginning of the game) are more probable to happen since they are more predictable than the long-term future reward.
    
- To solve an RL problem, you want to **find an optimal policy**; the policy is the “brain” of your AI that will tell us what action to take given a state. The optimal one is the one that gives you the actions that max the expected return.

There are **two** ways to find your optimal policy:

- By **training your policy directly**: policy-based methods.
    
- By **training a value function** that tells us the expected return the agent will get at each state and use this function to define our policy: value-based methods.
    
- Finally, we spoke about Deep RL because **we introduce deep neural networks to estimate the action to take (policy-based) or to estimate the value of a state (value-based) hence the name “deep.”**
    
## Let’s train our first Deep Reinforcement Learning agent and upload it to the Hub 🚀

## Install dependencies and create a virtual screen 🔽

The first step is to install the dependencies, we’ll install multiple ones.

- `gymnasium[box2d]`: Contains the LunarLander-v2 environment 🌛
- `stable-baselines3[extra]`: The deep reinforcement learning library.
- `huggingface_sb3`: Additional code for Stable-baselines3 to load and upload models from the Hugging Face 🤗 Hub.

To make things easier, we created a script to install all these dependencies.

```bash
apt install swig cmake
pip install -r https://raw.githubusercontent.com/huggingface/deep-rl-class/main/notebooks/unit1/requirements-unit1.txt
```

During the notebook, we’ll need to generate a replay video. To do so, with colab, **we need to have a virtual screen to be able to render the environment** (and thus record the frames).

Hence the following cell will install virtual screen libraries and create and run a virtual screen 🖥.

```bash
sudo apt-get update
apt install python-opengl
apt install ffmpeg
apt install xvfb
pip3 install pyvirtualdisplay
```

To make sure the new installed libraries are used, **sometimes it’s required to restart the notebook runtime**. The next cell will force the **runtime to crash, so you’ll need to connect again and run the code starting from here**. Thanks to this trick, **we will be able to run our virtual screen.**

```python
import os
os.kill(os.getpid(), 9)
```

```python
# Virtual display
from pyvirtualdisplay import Display

virtual_display = Display(visible=0, size=(1400, 900))
virtual_display.start()
```

## Import the packages 📦

One additional library we import is huggingface_hub **to be able to upload and download trained models from the hub**.

The Hugging Face Hub 🤗 works as a central place where anyone can share and explore models and datasets. It has versioning, metrics, visualizations and other features that will allow you to easily collaborate with others.

You can see here all the Deep reinforcement Learning models available here👉 https://huggingface.co/models?pipeline_tag=reinforcement-learning&sort=downloads

```python
import gymnasium

from huggingface_sb3 import load_from_hub, package_to_hub
from huggingface_hub import (
    notebook_login,
)  # To log to our Hugging Face account to be able to upload models to the Hub.

from stable_baselines3 import PPO
from stable_baselines3.common.env_util import make_vec_env
from stable_baselines3.common.evaluation import evaluate_policy
from stable_baselines3.common.monitor import Monitor
```

## Understand Gymnasium and how it works 🤖

🏋 The library containing our environment is called Gymnasium. **You’ll use Gymnasium a lot in Deep Reinforcement Learning.**

Gymnasium is the **new version of Gym library** [maintained by the Farama Foundation](https://farama.org/).

The Gymnasium library provides two things:

- An interface that allows you to **create RL environments**.
- A **collection of environments** (gym-control, atari, box2D…).

Let’s look at an example, but first let’s recall the RL loop.
![The RL process](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/RL_process_game.jpg)

At each step:
- Our Agent receives a **state (S0)** from the **Environment** — we receive the first frame of our game (Environment).
- Based on that **state (S0),** the Agent takes an **action (A0)** — our Agent will move to the right.
- The environment transitions to a **new** **state (S1)** — new frame.
- The environment gives some **reward (R1)** to the Agent — we’re not dead _(Positive Reward +1)_.

With Gymnasium:

1️⃣ We create our environment using `gymnasium.make()`
2️⃣ We reset the environment to its initial state with `observation = env.reset()`

At each step:

3️⃣ Get an action using our model (in our example we take a random action)
4️⃣ Using `env.step(action)`, we perform this action in the environment and get

- `observation`: The new state (st+1)
- `reward`: The reward we get after executing the action
- `terminated`: Indicates if the episode terminated (agent reach the terminal state)
- `truncated`: Introduced with this new version, it indicates a timelimit or if an agent go out of bounds of the environment for instance.
- `info`: A dictionary that provides additional information (depends on the environment).

For more explanations check this 👉 [https://gymnasium.farama.org/api/env/#gymnasium.Env.step](https://gymnasium.farama.org/api/env/#gymnasium.Env.step)

If the episode is terminated:
- We reset the environment to its initial state with `observation = env.reset()`

**Let’s look at an example!** Make sure to read the code:

```python
import gymnasium as gym

# First, we create our environment called LunarLander-v2
env = gym.make("LunarLander-v2")

# Then we reset this environment
observation, info = env.reset()

for _ in range(20):
    # Take a random action
    action = env.action_space.sample()
    print("Action taken:", action)

    # Do this action in the environment and get
    # next_state, reward, terminated, truncated and info
    observation, reward, terminated, truncated, info = env.step(action)

    # If the game is terminated (in our case we land, crashed) or truncated (timeout)
    if terminated or truncated:
        # Reset the environment
        print("Environment is reset")
        observation, info = env.reset()

env.close()
```

## Create the LunarLander environment 🌛 and understand how it works

### The environment 🎮

In this first tutorial, we’re going to train our agent, a [Lunar Lander](https://gymnasium.farama.org/environments/box2d/lunar_lander/), **to land correctly on the moon**. To do that, the agent needs to learn **to adapt its speed and position (horizontal, vertical, and angular) to land correctly.**

💡 A good habit when you start to use an environment is to check its documentation 👉 [https://gymnasium.farama.org/environments/box2d/lunar_lander/](https://gymnasium.farama.org/environments/box2d/lunar_lander/)

Let’s see what the Environment looks like:

```python
# We create our environment with gym.make("<name_of_the_environment>")
env = gym.make("LunarLander-v2")
env.reset()
print("_____OBSERVATION SPACE_____ \n")
print("Observation Space Shape", env.observation_space.shape)
print("Sample observation", env.observation_space.sample())  # Get a random observation
```

We see with `Observation Space Shape (8,)` that the observation is a vector of size 8, where each value contains different information about the lander:

- Horizontal pad coordinate (x)
- Vertical pad coordinate (y)
- Horizontal speed (x)
- Vertical speed (y)
- Angle
- Angular speed
- If the left leg contact point has touched the land (boolean)
- If the right leg contact point has touched the land (boolean)

```python
print("\n _____ACTION SPACE_____ \n")
print("Action Space Shape", env.action_space.n)
print("Action Space Sample", env.action_space.sample())  # Take a random action
```

The action space (the set of possible actions the agent can take) is discrete with 4 actions available 🎮:

- Action 0: Do nothing,
- Action 1: Fire left orientation engine,
- Action 2: Fire the main engine,
- Action 3: Fire right orientation engine.

Reward function (the function that will gives a reward at each timestep) 💰:

After every step a reward is granted. The total reward of an episode is the **sum of the rewards for all the steps within that episode**.

For each step, the reward:

- Is increased/decreased the closer/further the lander is to the landing pad.
- Is increased/decreased the slower/faster the lander is moving.
- Is decreased the more the lander is tilted (angle not horizontal).
- Is increased by 10 points for each leg that is in contact with the ground.
- Is decreased by 0.03 points each frame a side engine is firing.
- Is decreased by 0.3 points each frame the main engine is firing.

The episode receive an **additional reward of -100 or +100 points for crashing or landing safely respectively.**

An episode is **considered a solution if it scores at least 200 points.**

#### Vectorized Environment

- We create a vectorized environment (a method for stacking multiple independent environments into a single environment) of 16 environments, this way, **we’ll have more diverse experiences during the training.**

```python
# Create the environment
env = make_vec_env("LunarLander-v2", n_envs=16)
```

## Create the Model 🤖

- We have studied our environment and we understood the problem: **being able to land the Lunar Lander to the Landing Pad correctly by controlling left, right and main orientation engine**. Now let’s build the algorithm we’re going to use to solve this Problem 🚀.
    
- To do so, we’re going to use our first Deep RL library, [Stable Baselines3 (SB3)](https://stable-baselines3.readthedocs.io/en/master/).
    
- SB3 is a set of **reliable implementations of reinforcement learning algorithms in PyTorch**.

💡 A good habit when using a new library is to dive first on the documentation: [https://stable-baselines3.readthedocs.io/en/master/](https://stable-baselines3.readthedocs.io/en/master/) and then try some tutorials.

To solve this problem, we’re going to use SB3 **PPO**. [PPO (aka Proximal Policy Optimization) is one of the SOTA (state of the art) Deep Reinforcement Learning algorithms that you’ll study during this course](https://stable-baselines3.readthedocs.io/en/master/modules/ppo.html#example%5D).

PPO is a combination of:

- _Value-based reinforcement learning method_: learning an action-value function that will tell us the **most valuable action to take given a state and action**.
- _Policy-based reinforcement learning method_: learning a policy that will **give us a probability distribution over actions**.

Stable-Baselines3 is easy to set up:

1️⃣ You **create your environment** (in our case it was done above)

2️⃣ You define the **model you want to use and instantiate this model** `model = PPO("MlpPolicy")`

3️⃣ You **train the agent** with `model.learn` and define the number of training timesteps.

```python
# Create environment
env = gym.make('LunarLander-v2')

# Instantiate the agent
model = PPO('MlpPolicy', env, verbose=1)
# Train the agent
model.learn(total_timesteps=int(2e5))
```

```python
# TODO: Define a PPO MlpPolicy architecture
# We use MultiLayerPerceptron (MLPPolicy) because the input is a vector,
# if we had frames as input we would use CnnPolicy
model = PPO(
    policy="MlpPolicy",
    env=env,
    n_steps=1024,
    batch_size=64,
    n_epochs=4,
    gamma=0.999,
    gae_lambda=0.98,
    ent_coef=0.01,
    verbose=1,
)
```

## Train the PPO agent 🏃

- Let’s train our agent for 1,000,000 timesteps, don’t forget to use GPU on Colab. It will take approximately ~20min, but you can use fewer timesteps if you just want to try it out.
- During the training, take a ☕ break you deserved it 🤗

```python
# Train it for 1,000,000 timesteps
model.learn(total_timesteps=1000000)
# Save the model
model_name = "ppo-LunarLander-v2"
model.save(model_name)
```

## Evaluate the agent 📈

- Remember to wrap the environment in a [Monitor](https://stable-baselines3.readthedocs.io/en/master/common/monitor.html).
- Now that our Lunar Lander agent is trained 🚀, we need to **check its performance**.
- Stable-Baselines3 provides a method to do that: `evaluate_policy`.
- To fill that part you need to [check the documentation](https://stable-baselines3.readthedocs.io/en/master/guide/examples.html#basic-usage-training-saving-loading)
- In the next step, we’ll see **how to automatically evaluate and share your agent to compete in a leaderboard, but for now let’s do it ourselves**

💡 When you evaluate your agent, you should not use your training environment but create an evaluation environment.

```python
eval_env = Monitor(gym.make("LunarLander-v2"))
mean_reward, std_reward = evaluate_policy(model, eval_env, n_eval_episodes=10, deterministic=True)
print(f"mean_reward={mean_reward:.2f} +/- {std_reward}")
```

- In my case, I got a mean reward is `200.20 +/- 20.80` after training for 1 million steps, which means that our lunar lander agent is ready to land on the moon 🌛🥳.

## Publish our trained model on the Hub 🔥

Now that we saw we got good results after the training, we can publish our trained model on the hub 🤗 with one line of code.

📚 The libraries documentation 👉 [https://github.com/huggingface/huggingface_sb3/tree/main#hugging-face—x-stable-baselines3-v20](https://github.com/huggingface/huggingface_sb3/tree/main#hugging-face--x-stable-baselines3-v20)

Here’s an example of a Model Card (with Space Invaders):

By using `package_to_hub` **you evaluate, record a replay, generate a model card of your agent and push it to the hub**.

This way:

- You can **showcase our work** 🔥
- You can **visualize your agent playing** 👀
- You can **share with the community an agent that others can use** 💾
- You can **access a leaderboard 🏆 to see how well your agent is performing compared to your classmates** 👉 [https://huggingface.co/spaces/huggingface-projects/Deep-Reinforcement-Learning-Leaderboard](https://huggingface.co/spaces/huggingface-projects/Deep-Reinforcement-Learning-Leaderboard)

To be able to share your model with the community there are three more steps to follow:

1️⃣ (If it’s not already done) create an account on Hugging Face ➡ [https://huggingface.co/join](https://huggingface.co/join)
2️⃣ Sign in and then, you need to store your authentication token from the Hugging Face website.

- Create a new token ([https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)) **with write role**

![Create HF Token](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/notebooks/create-token.jpg)

- Copy the token
- Run the cell below and paste the token

```python
notebook_login()
!git config --global credential.helper store
```

If you don’t want to use a Google Colab or a Jupyter Notebook, you need to use this command instead: `huggingface-cli login`

3️⃣ We’re now ready to push our trained agent to the 🤗 Hub 🔥 using `package_to_hub()` function

Let’s fill the `package_to_hub` function:

- `model`: our trained model.
- `model_name`: the name of the trained model that we defined in `model_save`
- `model_architecture`: the model architecture we used, in our case PPO
- `env_id`: the name of the environment, in our case `LunarLander-v2`
- `eval_env`: the evaluation environment defined in eval_env
- `repo_id`: the name of the Hugging Face Hub Repository that will be created/updated `(repo_id = {username}/{repo_name})`

💡 **A good name is `{username}/{model_architecture}-{env_id}`**

- `commit_message`: message of the commit

```python
import gymnasium as gym
from stable_baselines3.common.vec_env import DummyVecEnv
from stable_baselines3.common.env_util import make_vec_env

from huggingface_sb3 import package_to_hub

## TODO: Define a repo_id
## repo_id is the id of the model repository from the Hugging Face Hub (repo_id = {organization}/{repo_name} for instance ThomasSimonini/ppo-LunarLander-v2
repo_id = "DenCT/ppo-lunarlander-v2"

# TODO: Define the name of the environment
env_id = "LunarLander-v2"

# Create the evaluation env and set the render_mode="rgb_array"
eval_env = DummyVecEnv([lambda: gym.make(env_id, render_mode="rgb_array")])

# TODO: Define the model architecture we used
model_architecture = "PPO"

## TODO: Define the commit message
commit_message = "Initial commit"

# method save, evaluate, generate a model card and record a replay video of your agent before pushing the repo to the hub
package_to_hub(model=model, # Our trained model
               model_name=model_name, # The name of our trained model 
               model_architecture=model_architecture, # The model architecture we used: in our case PPO
               env_id=env_id, # Name of the environment
               eval_env=eval_env, # Evaluation Environment
               repo_id=repo_id, # id of the model repository from the Hugging Face Hub (repo_id = {organization}/{repo_name} for instance ThomasSimonini/ppo-LunarLander-v2
               commit_message=commit_message)
```

Congrats 🥳 you’ve just trained and uploaded your first Deep Reinforcement Learning agent. The script above should have displayed a link to a model repository such as [https://huggingface.co/osanseviero/test_sb3](https://huggingface.co/osanseviero/test_sb3). When you go to this link, you can:

- See a video preview of your agent at the right.
- Click “Files and versions” to see all the files in the repository.
- Click “Use in stable-baselines3” to get a code snippet that shows how to load the model.
- A model card (`README.md` file) which gives a description of the model

Under the hood, the Hub uses git-based repositories (don’t worry if you don’t know what git is), which means you can update the model with new versions as you experiment and improve your agent.

Compare the results of your LunarLander-v2 with your classmates using the leaderboard 🏆 👉 [https://huggingface.co/spaces/huggingface-projects/Deep-Reinforcement-Learning-Leaderboard](https://huggingface.co/spaces/huggingface-projects/Deep-Reinforcement-Learning-Leaderboard)
## Load a saved LunarLander model from the Hub 🤗

Thanks to [ironbar](https://github.com/ironbar) for the contribution.
Loading a saved model from the Hub is really easy.
You go to [https://huggingface.co/models?library=stable-baselines3](https://huggingface.co/models?library=stable-baselines3) to see the list of all the Stable-baselines3 saved models.

1. You select one and copy its repo_id

![Copy-id](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/notebooks/unit1/copy-id.png)

2. Then we just need to use load_from_hub with:

- The repo_id
- The filename: the saved model inside the repo and its extension (*.zip)

Because the model I download from the Hub was trained with Gym (the former version of Gymnasium) we need to install shimmy a API conversion tool that will help us to run the environment correctly.

Shimmy Documentation: [https://github.com/Farama-Foundation/Shimmy](https://github.com/Farama-Foundation/Shimmy)

```python
!pip install shimmy
```

```python
from huggingface_sb3 import load_from_hub

repo_id = "Classroom-workshop/assignment2-omar"  # The repo_id
filename = "ppo-LunarLander-v2.zip"  # The model filename.zip

# When the model was trained on Python 3.8 the pickle protocol is 5
# But Python 3.6, 3.7 use protocol 4
# In order to get compatibility we need to:
# 1. Install pickle5 (we done it at the beginning of the colab)
# 2. Create a custom empty object we pass as parameter to PPO.load()
custom_objects = {
    "learning_rate": 0.0,
    "lr_schedule": lambda _: 0.0,
    "clip_range": lambda _: 0.0,
}

checkpoint = load_from_hub(repo_id, filename)
model = PPO.load(checkpoint, custom_objects=custom_objects, print_system_info=True)
```

Let’s evaluate this agent:

```python
eval_env = Monitor(gym.make("LunarLander-v2"))
mean_reward, std_reward = evaluate_policy(model, eval_env, n_eval_episodes=10, deterministic=True)
print(f"mean_reward={mean_reward:.2f} +/- {std_reward}")
```

## Some additional challenges 🏆

The best way to learn **is to try things by your own**! As you saw, the current agent is not doing great. As a first suggestion, you can train for more steps. With 1,000,000 steps, we saw some great results!

In the [Leaderboard](https://huggingface.co/spaces/huggingface-projects/Deep-Reinforcement-Learning-Leaderboard) you will find your agents. Can you get to the top?

Here are some ideas to achieve so:

- Train more steps
- Try different hyperparameters for `PPO`. You can see them at [https://stable-baselines3.readthedocs.io/en/master/modules/ppo.html#parameters](https://stable-baselines3.readthedocs.io/en/master/modules/ppo.html#parameters).
- Check the [Stable-Baselines3 documentation](https://stable-baselines3.readthedocs.io/en/master/modules/dqn.html) and try another model such as DQN.
- **Push your new trained model** on the Hub 🔥

**Compare the results of your LunarLander-v2 with your classmates** using the [leaderboard](https://huggingface.co/spaces/huggingface-projects/Deep-Reinforcement-Learning-Leaderboard) 🏆

Is moon landing too boring for you? Try to **change the environment**, why not use MountainCar-v0, CartPole-v1 or CarRacing-v0? Check how they work [using the gym documentation](https://www.gymlibrary.dev/) and have fun 🎉.

Congrats on finishing this chapter! That was the biggest one, **and there was a lot of information.**

If you’re still feel confused with all these elements…it’s totally normal! **This was the same for me and for all people who studied RL.**

Take time to really **grasp the material before continuing and try the additional challenges**. It’s important to master these elements and have a solid foundations.

Naturally, during the course, we’re going to dive deeper into these concepts but **it’s better to have a good understanding of them now before diving into the next chapters.**

Next time, in the bonus unit 1, you’ll train Huggy the Dog to fetch the stick.

## Quiz

### 1: What is Reinforcement Learning?
Reinforcement learning is a **framework for solving control tasks (also called decision problems)** by building agents that learn from the environment by interacting with it through trial and error and **receiving rewards (positive or negative) as unique feedback**.
### 2: Define the RL Loop
![Exercise RL Loop](https://huggingface.co/datasets/huggingface-deep-rl-course/course-images/resolve/main/en/unit1/rl-loop-ex.jpg)

At every step:

- Our Agent receives **state s0** from the environment
- Based on that **state s0** the Agent takes an **action a0**
- Our Agent will move to the right
- The Environment goes to a **new state s1**
- The Environment gives a **reward r1** to the Agent
### 3: What’s the difference between a state and an observation?
- The state is a complete description of the state of the world (there is no hidden information)
- The observation is a partial description of the state
-  We receive a state when we play with chess environment
- We receive an observation when we play with Super Mario Bros
### 4: A task is an instance of a Reinforcement Learning problem. What are the two types of tasks?
- Episodic
- Continuing
### 5: What is the exploration/exploitation tradeoff?
In Reinforcement Learning, we need to **balance how much we explore the environment and how much we exploit what we know about the environment**.

- _Exploration_ is exploring the environment by **trying random actions in order to find more information about the environment**.
- _Exploitation_ is **exploiting known information to maximize the reward**.
### 6: What is a policy?
- The Policy π **is the brain of our Agent**. It’s the function that tells us what action to take given the state we are in. So it defines the agent’s behavior at a given time.
### 7: What are value-based methods?
- Value-based methods is one of the main approaches for solving RL problems.
- In Value-based methods, instead of training a policy function, **we train a value function that maps a state to the expected value of being at that state**.
### 8: What are policy-based methods?
- In _Policy-Based Methods_, we learn a **policy function directly**.
- This policy function will **map from each state to the best corresponding action at that state**. Or a **probability distribution over the set of possible actions at that state**.