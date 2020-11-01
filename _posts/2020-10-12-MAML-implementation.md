---
title: "One-shot Visual Imitation Learning via Meta-learning"
categories:
  - paper review
tags:
  - visual imitation
  - meta learning
---

# 1. tensorflow 1을 써야할때
import tensorflow.compat.v1 as tf
tf.disable_v2_behavior()

---

string_input_producer (from tensorflow.python.training.input) is deprecated and will be removed in a future version.
Instructions for updating:
Queue-based input pipelines have been replaced by `tf.data`. Use `tf.data.Dataset.from_tensor_slices(string_tensor).shuffle(tf.shape(input_tensor, out_type=tf.int64)[0]).repeat(num_epochs)`. If `shuffle=False`, omit the `.shuffle(...)`.

limit_epochs (from tensorflow.python.training.input) is deprecated and will be rem                oved in a future version.
QueueRunner.__init__ (from tensorflow.python.training.queue_runner_impl) is deprec                ated and will be removed in a future version.
WholeFileReader.__init__ (from tensorflow.python.ops.io_ops) is deprecated and will be removed in a future version.
batch (from tensorflow.python.training.input) is deprecated and will be removed in a future version.


# 2. pipfile이 설치 관련 버전인듯

ValueError: Tried to convert 'indices' to a tensor and failed. Error: Argument must be a dense tensor: range(0, 20) - got shape [20], but wanted [].
  
  --> list(range()) 로 바꾸기!
  


  


