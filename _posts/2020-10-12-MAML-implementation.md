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

WARNING:tensorflow:From /home/hskim/mil/data_generator.py:195: string_input_producer (from tensorflow                .python.training.input) is deprecated and will be removed in a future version.
Instructions for updating:
Queue-based input pipelines have been replaced by `tf.data`. Use `tf.data.Dataset.from_tensor_slices(                string_tensor).shuffle(tf.shape(input_tensor, out_type=tf.int64)[0]).repeat(num_epochs)`. If `shuffle                =False`, omit the `.shuffle(...)`.
WARNING:tensorflow:From /home/hskim/anaconda3/lib/python3.7/site-packages/tensorflow_core/python/trai                ning/input.py:277: input_producer (from tensorflow.python.training.input) is deprecated and will be r                emoved in a future version.
Instructions for updating:
Queue-based input pipelines have been replaced by `tf.data`. Use `tf.data.Dataset.from_tensor_slices(                input_tensor).shuffle(tf.shape(input_tensor, out_type=tf.int64)[0]).repeat(num_epochs)`. If `shuffle=                False`, omit the `.shuffle(...)`.
WARNING:tensorflow:From /home/hskim/anaconda3/lib/python3.7/site-packages/tensorflow_core/python/trai                ning/input.py:189: limit_epochs (from tensorflow.python.training.input) is deprecated and will be rem                oved in a future version.
Instructions for updating:
Queue-based input pipelines have been replaced by `tf.data`. Use `tf.data.Dataset.from_tensors(tensor                ).repeat(num_epochs)`.
WARNING:tensorflow:From /home/hskim/anaconda3/lib/python3.7/site-packages/tensorflow_core/python/trai                ning/input.py:198: QueueRunner.__init__ (from tensorflow.python.training.queue_runner_impl) is deprec                ated and will be removed in a future version.
Instructions for updating:
To construct input pipelines, use the `tf.data` module.
WARNING:tensorflow:From /home/hskim/anaconda3/lib/python3.7/site-packages/tensorflow_core/python/trai                ning/input.py:198: add_queue_runner (from tensorflow.python.training.queue_runner_impl) is deprecated                 and will be removed in a future version.
Instructions for updating:
To construct input pipelines, use the `tf.data` module.
Generating image processing ops
WARNING:tensorflow:From /home/hskim/mil/data_generator.py:197: WholeFileReader.__init__ (from tensorf                low.python.ops.io_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Queue-based input pipelines have been replaced by `tf.data`. Use `tf.data.Dataset.map(tf.read_file)`.
Batching images
WARNING:tensorflow:From /home/hskim/mil/data_generator.py:226: batch (from tensorflow.python.training                .input) is deprecated and will be removed in a future version.
Instructions for updating:
Queue-based input pipelines have been replaced by `tf.data`. Use `tf.data.Dataset.batch(batch_size)`                 (or `padded_batch(...)` if `dynamic_pad=True`).


# 2. pipfile이 설치 관련 버전인듯


 File "/home/hskim/mil/mil.py", line 254, in forward
    context = tf.transpose(tf.gather(tf.transpose(tf.zeros_like(flatten_image)), range(FLAGS.bt_dim))) 
ValueError: Tried to convert 'indices' to a tensor and failed. Error: Argument must be a dense tensor: range(0, 20) - got shape [20], but wanted [].
  
  --> list(range()) 로 바꾸기!
  
  File "/home/hskim/mil/mil.py", line 530, in batch_metalearn
    grads = tf.gradients(local_lossa, weights.values())

TypeError: Failed to convert object of type <class 'dict_values'> to Tensor. Contents: dict_values([<tf.Tensor 'model/clip_by_value:0' shape=(125, 125, 3) dtype=float32>, <tf.Variable 'model/wc1:0' shape=(5, 5, 6, 16) dtype=float32_ref>, <tf.Variable 'model/bc1:0' shape=(16,) dtype=float32_ref>, <tf.Variable 'model/wc2:0' shape=(5, 5, 16, 16) dtype=float32_ref>, <tf.Variable 'model/bc2:0' shape=(16,) dtype=float32_ref>, <tf.Variable 'model/wc3:0' shape=(5, 5, 16, 16) dtype=float32_ref>, <tf.Variable 'model/bc3:0' shape=(16,) dtype=float32_ref>, <tf.Variable 'model/wc4:0' shape=(5, 5, 16, 16) dtype=float32_ref>, <tf.Variable 'model/bc4:0' shape=(16,) dtype=float32_ref>, <tf.Variable 'model/context:0' shape=(20,) dtype=float32_ref>, <tf.Variable 'model/w_0:0' shape=(72, 200) dtype=float32_ref>, <tf.Variable 'model/b_0:0' shape=(200,) dtype=float32_ref>, <tf.Variable 'model/w_1:0' shape=(200, 200) dtype=float32_ref>, <tf.Variable 'model/b_1:0' shape=(200,) dtype=float32_ref>, <tf.Variable 'model/w_2:0' shape=(200, 7) dtype=float32_ref>, <tf.Variable 'model/b_2:0' shape=(7,) dtype=float32_ref>, <tf.Variable 'model/w_2_two_heads:0' shape=(200, 7) dtype=float32_ref>, <tf.Variable 'model/b_2_two_heads:0' shape=(7,) dtype=float32_ref>]). Consider casting elements to a supported type.

  


