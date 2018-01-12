---
layout: post
title:  "urlib urlopen 一个https自签名证书时ssl证书错误"
date:   2018-1-11 14:31:25 +0800
categories: python
---
当你urllib.urlopen一个 https 的时候会验证一次 SSL 证书
当目标使用的是自签名的证书时就会爆出一个
URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:581)> 的错误消息，

解决方案包括下列两种方式：
1. 使用ssl创建未经验证的上下文，在urlopen中传入上下文参数
{% highlight python %}
import ssl
import urllib
import urllib.request

context = ssl._create_unverified_context()
print urllib.request.urlopen(target_url, context=context).read()
{% endhighlight %}

2. 全局取消证书验证
{% highlight python %}
import ssl
import urllib
import urllib.request

ssl._create_default_https_context = ssl._create_unverified_context
print urllib.request.urlopen(target_url).read()
{% endhighlight %}

