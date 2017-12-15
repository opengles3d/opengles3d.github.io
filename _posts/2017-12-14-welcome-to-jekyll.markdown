---
layout: post
title:  "Welcome to Jekyll!"
date:   2017-12-14 14:31:25 +0800
categories: jekyll update
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

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
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
