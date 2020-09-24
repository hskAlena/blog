---
title: "Imitation from Observation: Learning to Imitate Behaviors from Raw Video via Context Translation"
date: 2020-09-23T13:34:30-16:00
categories:
  - paper review
tags:
  - visual imitation learning
  - raw video
  - context translation
use_math: true
---

abstract
===
사람들은 changes in viewpoint, surroundings, object positions and types, and other factors에 상관없이 다른 사람의 행동을 보고 따라할 수 있다.
-> video prediction with context translation and deep reinforcement learning을 이용해 문제를 풀어보겠다.
  
introduction
===
보통 autonomous agent가 skill을 배울 때 reward function(어떤 state와 action이 desirable한지), expert demonstration을 가지고 배우는데, 
 reward function은 hand-crafted라서 complex observation이 필요한 task에선 적절한 것을 찾기 어렵다.
Expert demonstration을 가지고 배우는 imitation learning은 Behavior cloning과 Inverse reinforcement learning으로 나뉘는데, 
 observation-action tuple을 가지고 배우는 거라 실생활과 거리가 있었다. 우리는 ego-centric observation과 ground truth action을 받으면서 보고 배우진 않으니까.
  
![Figure 1](/assets/images/ifo_context_fig1.png)

Imitation-from-observation algorithm은 context translation model(third person view & human demo -> first person view & robot)에 based 되어있다.
 tracking demo behavior를 위한 Feature representation이 필요하고, deep RL로 action optimize를 한다. translation method는 useful perceptual rewrd function을 제공할 수 있다.
다른 연구에서는 invariant feature space를 구한다든가, adversarial imitation learning, track pre-trained visual feature을 하는데 우리것이 제일 robust하다. 
  
Related work
===
Imitation Learning이란?
- learning a policy that generalizes to unseen states
  - helicopter flight trhough apprenticeship learning
  - put a ball in a cup and playing table tennis
  - human-like reaching motions
** teleoperation or kinesthetic teaching **
 
Imitation Learning을 methodological하게 나눠보면:
- behavior cloning (supervised learning)
 - imitation-from-observation 환경에서는  action이 주어지지 않고 different context이기 때문에 direct behavior cloning을 못한대.
- inverse reinforcement learning (IRL)
 - expert demo에서 reward function 유추하고 RL을 통해 policy recovery하는 경우인데, image같은 high-dimensional observation에서는 쓰기 어렵대.

지금까지 비슷한 문제들(context differ관점에서)을 해결하려했던 논문들은
1. expert와 non-expert policy를 직접 비교하고 complex manipulation task를 못한다.
2. pretrained visual feature가 context가 바뀌어도 invariance를 가지는 것에 착안하여 한것. (context에 대한 고려 부족)
3. invariance of visual features through multi-viewpoint 
4. first-person video of human에서 hand detection하고 vision pipeline 따라서 하는것.
 - 하지만 우리것은 end-to-end training이고 prior visual feature, detectors, vision systems가 필요없다.
5. paired examples of state sequences을 이용해서 policy training - low-dimension에서만 하고, context shift가 없다.
 - 우리것은 action도 필요없고 raw observation으로도 충분하다 
 
우리의 technical approach처럼 visual domain adaptation, image translation 하려했던 논문들은,
- pixel level domain adaptation 
- translation of visual style between domains using GAN, 
 - translating demonstrations from one context to another - GAN 쓰면 더 향상되긴 할거야.

Tasks : sweeping, pushing, pouring, striking
- low cost tool attachment & kinesthetic programming by demonstration (sweeping)
- simple PID controller with specified objective volume (pouring) -> inferring objective from demo
- predictive models on point-cloud data and uses a significantly different intuitive physics model with depth data. (pushing)

problem formulation and overview
===
  
"context" includes "viewpoint, background, positions, identities of object in the environment"

Demonstrations $\{D_1, D_2, ... D_n\} = \{[o^{1}_{0}, o^{1}_{1}, ..., o^{1}_{T}], ... [o^{n}_{0}, o^{n}_{1}, ..., o^{n}_{T}]\}$
consist of observations $o_t$ partially observed Markove process governed by 
an observation distribution $p(o_t | s_t, w)$, dynamics $p(s_{t+1} | s_t, a_t, w)$, 
and the expert's policy $p(a_t | s_t, w)$, each demo in different context $w$. $w$ is sampled independently from $p(w)$.
$o^{i}_{t}$ refer to observation at time $t$ from context $w$.

사실 learner's context는 demo's context와 다를테지만(body가 다르니), $p(w)$가 동일하다고 친다.
두개의 challenge가 있다. 
1. observation에서 어떤 information을 track할지 정해야한다. 내 context $w_l$와 demo거는 다르니까.
2. 어떤 action이 demo observation을 track할 수 있는지 정해야한다. -> RL (demo와의 거리를 reward로 잡고 그 distance 좁히는 action)
 - observation이 raw image pixel일땐 Euclidean distance는 well-shaped objective가 아닐듯.(semantically meaningful한가)
 - 첫번째 문제의 해결점인 'context mismatch'가 distance metric 고르는데 도움준다. -> different demo를 training data로 넣고 context 바꾸는걸 학습하여 해결.
 - proper context translation은 underlying factors of variation을 알아야한다. 
 - squared Euclidean distance between features of context translation model as a reward function
 
Learning to translate between contexts
===

