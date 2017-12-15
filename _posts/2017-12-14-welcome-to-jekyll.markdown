---
layout: post
title:  "Tensorflow Iterator does not have an initializer"
date:   2017-12-14 14:31:25 +0800
categories: python
---
Tensorflow Iterator does not have an initializer

{% highlight python %}
import tensorflow as tf
training_dataset = tf.data.Dataset.range(100).map(lambda x: x + tf.random_uniform([],-10, 10, tf.int64)).repeat()
validation_dataset = tf.data.Dataset.range(50)

handle = tf.placeholder(tf.string, shape=[])
iterator = tf.contrib.data.Iterator.from_string_handle(handle, training_dataset.output_types, training_dataset.output_shapes)
next_element = iterator.get_next()

training_iterator = training_dataset.make_initializable_iterator()
validation_iterator = validation_dataset.make_initializable_iterator()

with tf.Session() as sess:
    training_handle = sess.run(training_iterator.string_handle())
    validation_handle = sess.run(validation_iterator.string_handle())
    while True:
        sess.run(training_iterator.initializer)
        for _ in range(200):
            sess.run(next_element, feed_dict={handle:training_handle})
        sess.run(validation_iterator.initializer)
        for _ in range(50):
            print(sess.run(next_element, feed_dict={handle:validation_handle}))
{% endhighlight %}

If you use training_dataset.make_one_shot_iterator() to get a iterator,you will got "Iterator does not have an initializer" error.

