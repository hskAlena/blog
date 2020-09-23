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

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
