
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "scrolled": true
   },
   "outputs": [],
   "source": [
    "!pip install gym[box2d] box2d-py swig gymnasium stable_baselines3[extra] box2d box2d-kengz ipywidgets ffmpeg"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "scrolled": true
   },
   "outputs": [],
   "source": [
    "import gymnasium as gym\n",
    "from stable_baselines3 import PPO\n",
    "from stable_baselines3.common.evaluation import evaluate_policy\n",
    "\n",
    "# Create environment\n",
    "env = gym.make(\"LunarLander-v2\", render_mode=\"rgb_array\")\n",
    "\n",
    "# Instantiate the agent\n",
    "model = PPO(\n",
    "    'MlpPolicy',\n",
    "    env,\n",
    "    verbose=1,\n",
    "    ##### HYPERPARAMETERS HERE!!!!\n",
    "    learning_rate=0.001,\n",
    "    batch_size=32,\n",
    "    )\n",
    "\n",
    "# Train the agent and display a progress bar\n",
    "model.learn(total_timesteps=int(10000), progress_bar=True)\n",
    "\n",
    "# Save the agent\n",
    "model.save(\"ppo_lunar\")\n",
    "#del model  # delete trained model to demonstrate loading"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "import gymnasium as gym\n",
    "from stable_baselines3 import PPO\n",
    "from stable_baselines3.common.evaluation import evaluate_policy\n",
    "import imageio\n",
    "import numpy as np\n",
    "\n",
    "# Load the trained agent\n",
    "env = gym.make(\"LunarLander-v2\", render_mode=\"rgb_array\")\n",
    "model = PPO.load(\"ppo_lunar\", env=env)\n",
    "\n",
    "# Evaluate the agent\n",
    "mean_reward, std_reward = evaluate_policy(model, model.get_env(), n_eval_episodes=10)\n",
    "print('Mean reward:', mean_reward, 'Std. reward:', std_reward)\n",
    "\n",
    "# Test the trained agent\n",
    "images = []\n",
    "j = 0\n",
    "vec_env = model.get_env()\n",
    "obs = vec_env.reset()\n",
    "img = model.env.render(mode=\"rgb_array\")\n",
    "for i in range(2000):\n",
    "    images.append(img)\n",
    "    action, _states = model.predict(obs, deterministic=True)\n",
    "    obs, rewards, dones, info = vec_env.step(action)\n",
    "    #vec_env.render()\n",
    "    if dones:\n",
    "        j = j + 1\n",
    "        print('Episode:', j, 'Rewards:', rewards, 'Info:', info, 'Dones:', dones)\n",
    "        imageio.mimsave(f\"./images/ppo_lander_{j}.gif\", [np.array(img) for k, img in enumerate(images) if k%2 == 0], fps=29)\n",
    "        images = []\n",
    "    img = model.env.render(mode=\"rgb_array\")\n",
    "vec_env.close()"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.6"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}