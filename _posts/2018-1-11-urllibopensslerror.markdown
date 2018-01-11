---
layout: post
title:  "urlib urlopen һ��https��ǩ��֤��ʱssl֤�����"
date:   2018-1-11 14:31:25 +0800
categories: python
---

����urllib.urlopenһ�� https ��ʱ�����֤һ�� SSL ֤��
��Ŀ��ʹ�õ�����ǩ����֤��ʱ�ͻᱬ��һ��
URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed (_ssl.c:581)> �Ĵ�����Ϣ��
������������������ַ�ʽ��
1. ʹ��ssl����δ����֤�������ģ���urlopen�д��������Ĳ���
{% highlight python %}
import ssl
import urllib
import urllib.request

context = ssl._create_unverified_context()
print urllib.request.urlopen(target_url, context=context).read()
{% endhighlight %}
2. ȫ��ȡ��֤����֤
{% highlight python %}
import ssl
import urllib
import urllib.request

ssl._create_default_https_context = ssl._create_unverified_context
print urllib.request.urlopen(target_url).read()
{% endhighlight %}

