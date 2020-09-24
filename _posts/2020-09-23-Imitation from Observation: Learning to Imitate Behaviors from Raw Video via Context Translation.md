---
title: "Imitation from Observation: Learning to Imitate Behaviors from Raw Video via Context Translation"
date: 2020-09-23T13:34:30-16:00
categories:
  - paper review
tags:
  - visual imitation learning
  - raw video
  - context translation
---

<abstract>
사람들은 changes in viewpoint, surroundings, object positions and types, and other factors에 상관없이 다른 사람의 행동을 보고 따라할 수 있다.
-> video prediction with context translation and deep reinforcement learning을 이용해 문제를 풀어보겠다.
  
<introduction>
보통 autonomous agent가 skill을 배울 때 reward function(어떤 state와 action이 desirable한지), expert demonstration을 가지고 배우는데, 
 reward function은 hand-crafted라서 complex observation이 필요한 task에선 적절한 것을 찾기 어렵다.
Expert demonstration을 가지고 배우는 imitation learning은 Behavior cloning과 Inverse reinforcement learning으로 나뉘는데, 
 observation-action tuple을 가지고 배우는 거라 실생활과 거리가 있었다. 우리는 ego-centric observation과 ground truth action을 받으면서 보고 배우진 않으니까.
  
Imitation-from-observation algorithm은 context translation model(third person view & human demo -> first person view & robot)에 based 되어있다.
 tracking demo behavior를 위한 Feature representation이 필요하고, deep RL로 action optimize를 한다. translation method는 useful perceptual rewrd function을 제공할 수 있다.
다른 연구에서는 invariant feature space를 구한다든가, adversarial imitation learning, track pre-trained visual feature을 하는데 우리것이 제일 robust하다. 
  
<Related work>
- learning a policy that generalizes to unseen states
 ex) - helicopter flight trhough apprenticeship learning
     - put a ball in a cup and playing table tennis
     - human-like reaching motions
 => teleoperation or kinesthetic teaching
  
- behavior cloning (supervised learning)
 -> imitation-from-observation 환경에서는  action이 주어지지 않고 different context이기 때문에 direct behavior cloning을 못한대.
- inverse reinforcement learning (IRL)
 -> expert demo에서 reward function 유추하고 RL을 통해 policy recovery하는 경우인데, image같은 high-dimensional observation에서는 쓰기 어렵대.
 
1. expert와 non-expert policy를 직접 비교하고 complex manipulation task를 못한다.
2. pretrained visual feature가 context가 바뀌어도 invariance를 가지는 것에 착안하여 한것. (context에 대한 고려 부족)
3. invariance of visual features through multi-viewpoint 
4. first-person video of human에서 hand detection하고 vision pipeline 따라서 하는것.
 => 하지만 우리것은 end-to-end training이고 prior visual feature, detectors, vision systems가 필요없다.
5. paired examples of state sequences을 이용해서 policy training - low-dimension에서만 하고, context shift가 없다.
 => 우리것은 action도 필요없고 raw observation으로도 충분하다 
 
1. pixel level domain adaptation 
2. translation of visual style between domains using GAN, 
-> translating demonstrations from one context to another - GAN 쓰면 더 향상되긴 할거야.

Tasks : sweeping, pushing, pouring, striking
1. low cost tool attachment & kinesthetic programming by demonstration (sweeping)
2. simple PID controller with specified objective volume (pouring) -> inferring objective from demo
3. predictive models on point-cloud data and uses a significantly different intuitive physics model with depth data. (pushing)

<problem formulation and overview>
  
"context" includes "viewpoint, background, positions, identities of object in the environment"
{D1, D2, ... Dn} = {[o1,
You'll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

```ruby
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
```

