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
---

# Model-based IfO

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

# ???
**LfO with Hand-crafted Reward and Forward RL**

- DeepMimic은 reward가 agent to directly match expert's physical proprieties(joint angles and velocities)하게 디자인하고, forward RL을 돌려서 policy를 배운다.
- reward function이 expert action을 고려하지 않기때문에 action에서 reward를 얻는 task는 해결하기 어렵다.

# model-free IfO
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

---

**learn time-dependent representation of tasks & hand-designed, time-aligned reward function**
- embedding function using triplet loss function으로 가까운 state는 붙이고 나머지는 떨어뜨리기.

**state representation handling viewpoint difference**

**shuffle-and-learn style loss로 task progress predict하는 neural network를 reward function으로**

**self-supervised objective로 embedding 배우고 current state와 demo의 checkpoint와의 차이를 reward function으로**

# plan/goal recognition through mirroring
- fixed controller를 이용해서 plan/goal infer인데,
- IfO에서는 controller도 배워야하니 기각.

