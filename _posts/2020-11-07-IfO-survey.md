---
title: "Recent Advances in imitation learning from observation"
excerpt_separator: "<!--more-->"
categories:
  - paper review
tags:
  - Imitation from observation
---

Previous imitation learning papers
---
- Movement imitation with nonlinear dynamical systems in humanoid robots.
- Humanoid robot learning and game playing using pc-based vision.

**visual observations can only provide partial state information**
**In imitation learning, agents do not recieve task reward feedback r.**

Behavior cloning does not require any further interaction between the agent and the environment / covariate shift problem
IRL-based techniques iteratively alternate between using demo to infer a hidden reward function and using RL.
- object manipulation : Guided cost learning: Deep inverse optimal control via policy optimization.
GAIL : induce an imitator state-action occupancy measure that is similar to that of the demonstrator.

Imitation learning from observation
===

##perception
1. Record the expert's movements using sensors placed directly on the expert agent
- Trajectory formation for imitation with nonlinear dynamical systems.
arm-reaching movements, biped locomotion and human gestures
- Incremental learning of gestures by imitation in a humanoid robot.

2. Motion capture: use visual markers on the demo to infer movement.
- Motion capture in robotics review.
locomotion, acrobatics, martial arts
- require costly instrumentation and pre-processing: A deep learning framework for character motion synthesis and editing.



##Control
