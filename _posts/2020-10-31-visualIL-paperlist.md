---
title: "visual imitation learning paper lists"
categories:
  - paper list
tags:
  - visual imitation
  - imitation from observation
  - learning from observation
---

# state-only demonstration


## Model-based IfO

**learn explicit model of environment**
- BCO infer exact action with learned inverse dynamics model. 그렇게 얻은 (s,a)로 BC 돌림. 
- inverse dynamics model은 현재 policy dependent하기 때문에 optimal policy를 알기 전까진 optimal inverse dynamics model을 알 수 없음.

**reinforced inverse dynamics modeling (RIDM)**
- exploration policy로 model of environment 배우고
- optimize model using sparse reward function

**imitating latent policies from observation (ILPO)**
- predict next state using latent policy and forward dynamics model
- predicted state와 actual demo를 비교해서 model과 imitation policy update
- environment와 상호작용하며 action label을 고침.

## ???
**LfO with Hand-crafted Reward and Forward RL**

- DeepMimic은 reward가 agent to directly match expert's physical proprieties(joint angles and velocities)하게 디자인하고, forward RL을 돌려서 policy를 배운다.
- reward function이 expert action을 고려하지 않기때문에 action에서 reward를 얻는 task는 해결하기 어렵다.

## plan/goal recognition through mirroring
- fixed controller를 이용해서 plan/goal infer인데,
- IfO에서는 controller도 배워야하니 기각.

## model-free IfO
**Imitation Learning from Observations by Minimizing Inverse Dynamics Disagreement**

- upper bound of gap between LfD and LfO is revealed by a negative causal entropy which can be minimized in a model-free way.
- inverse-dynamics-disagreement-minimization
- GAIfO와 가장 유사. 하지만 KL divergence로 disagreement를 측정한다.
- discriminator update 후에 policy를 (PPO) + MI + entropy + Q-value from discriminator 이용해 update한다.

**LfO with GAIL**

- GAIfO is similar to GAIL but has replaced state-action to state transition (s,a) -> (s,s')
- JS divergence

**adversarial domain confusion method**

**Imitation Learning from Video by Leveraging Proprioception**

- agent has access to their own internal states (proprioception)
- proprioceptive state representation 이랑 demo를 visually 비교하면서 policy 배우기.
- GAIfO에다가 proprioception 붙인거.

# Dealing with images


1. Time-contrastive networks: self-supervised learning from multi-view observation
  **learn time-dependent representation of tasks & hand-designed, time-aligned reward function**
  - embedding function using triplet loss function으로 가까운 state는 붙이고 나머지는 떨어뜨리기.

1. Imitation from observation: learning to imitate behavrios from raw video via context translation
  **state representation handling viewpoint difference**
  **video prediction with context translation and deep RL**
  - high-dimensional input인 image에 IRL을 적용하기는 힘들다.
  - visual domain adaptation & image translation
  1. limitation: demo가 많이 필요함. higher level representation을 갖다쓰면 좀 나을듯.
  2. limitation: demo가 multiple context에 필요하다. multiple task를 한 model로 배울 수 있다면 자동으로 multiple context가 갖춰질듯.
  3. future: explicit handling of domain shift가 보충되면 좋겠다.

1. One-shot learning of multi-step tasks from observation via activity localization in auxiliary video.
**shuffle-and-learn style loss로 task progress predict하는 neural network를 reward function으로**

1. Playing hard exploration games by watching youtube.
**self-supervised objective로 embedding 배우고 current state와 demo의 checkpoint와의 차이를 reward function으로**

1. Third-person imitation learning
   **domain shift, but access to expert and non-expert policy needed & optimize for invariance between only two contexts**
   **complex task는 잘 못함**
   
1. Unsupervised perceptual rewards for imitation learning
  **pretrained visual feature를 이용해 context difference를 해결하려함. inherent invariance of visual feature through multi-view point**
  
1. Learning robot activities from first-person human videos using convolutional future regression
  - explicit hand detection & engineered vision pipeline 통해서 first-person video of human보고 배움. (end-to-end가 안되고 prior visual feature, detector, vision system이 필요함)

1. One-shot imitation learning
  - paired state sequence를 policy에 넣어 학습. low-dimension에서만 가능하다.
  
## robotics?

1. Robobarista: Learning to manipulate novel objects via deep multimodal embedding

1. Deepmpc: Learning deep latent features for model predictive control

1. Se3-nets: Learning rigid body motion using deep neural networks.



