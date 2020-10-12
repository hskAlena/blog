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

