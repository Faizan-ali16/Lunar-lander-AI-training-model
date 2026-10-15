# Lunar Lander with PPO

A small project where I train an agent to land a rocket in Gymnasium's LunarLander-v3 using PPO (Stable-Baselines3), then change the reward to see what it does to the agent.

The video starts with the agent's first untrained attempt and goes up to clean landings. The score curve builds up on the side.

## What I did

I trained it three times with different rewards:

| Run | Reward | Avg score | Flights over 200 | Steps |
|---|---|---|---|---|
| 1. Time penalty | -0.01 per frame | 250.5 | 100/100 | 819,216 |
| 2. Hover bonus | +1 per frame if upright and slow | -1.0 | 0/100 | 1,015,808 |

All scores are from 100 test flights on the normal game with my reward changes turned off. 200 counts as solved.

Run 1 landed every time. I didn't pick the number of attempts. The agent gets tested on the normal game every ~50k steps and training stops once the average passes 240. It stopped at about 819k steps (2,648 attempts). I only set caps of 2M steps or 40 minutes so it couldn't run forever.

Run 2 was broken on purpose. Landing ends the episode, which also ends the +1 bonus, so hovering pays more than landing. The training score looked okay (around +90), but in the test flights it never landed.

## Setup

8 numbers per frame go in (position, speed, tilt, spin, leg contact) and 4 actions come out (nothing, left engine, main engine, right engine). 16 games run in parallel on CPU, no GPU.

## Running it

Open `lunar_lander_ppo.ipynb` in Colab and run the cells one at a time. Each run takes around 15-20 minutes.

I used an AI assistant to help write the notebook code.

https://github.com/user-attachments/assets/fc48acfb-6296-4e4f-9956-dfa43aeed9aa

