---
layout: post
title:  "宋词无关大数据,只关风和月"
date:   2017-12-18 14:31:25 +0800
categories: big data
---
宋词无关大数据,只关风和月.

{% highlight python %}
import jieba

STOPWORDS = []
PUNCTUATIONS = [u'\n',u' ',u',',u'-',u'【',u'】',u'。', u'，', u'“', u'”', u'…', u'？', u'！', u'、', u'；', u'（', u'）']

f_in = open('~/songci2.txt')

d = {}
try:
    for l in f_in:
        seg_list = jieba.cut(l)       
        for seg in seg_list:
            seg = seg.strip()
            if seg not in STOPWORDS and seg not in PUNCTUATIONS and len(seg) > 0:
                if seg in d:
                    k = d[seg]
                    d[seg] = k +1
                else:
                    d[seg] = 1
finally:
    f_in.close()

d = sorted(d.items(), key=lambda d: d[1], reverse=True)
for key in d:
    print(key[0], ":", key[1])

{% endhighlight %}

东风: 33
黄昏: 26
斜阳: 22
何处: 22
风雨: 22
天涯: 21
相思: 21
归来: 21
无人: 20
千里: 20
阑干: 20
芳草: 19
明月: 18
流水: 16
春风: 16
多少: 16
凄凉: 15
如今: 14
惟有: 14
相逢: 14
清明: 14
江南: 13
酒醒: 13
去年: 13
寂寞: 12
那堪: 12
断肠: 12
几许: 12
归去: 12
人间: 12
秋千: 11
回首: 11
当时: 11
双燕: 11
西风: 11
行人: 11
消魂: 11
无情: 10
春梦: 10
来时: 10
西楼: 10
故人: 10
天气: 10
时节: 10


又 : 74
月 : 58
谁 : 57
去 : 56
还 : 55
有 : 53
恨 : 48
是 : 46
与 : 43
更 : 43
在 : 42
处 : 40
无 : 40
也 : 40
人 : 39
不 : 38
东风 : 37
都 : 37
春 : 36
梦 : 33
年 : 32
雨 : 31
说 : 31
却 : 30
到 : 29
但 : 29
尽 : 28
见 : 28
酒 : 28
欲 : 28
怕 : 27
归 : 26
暮 : 26
了 : 26
黄昏 : 26
斜阳 : 25
来 : 25
倚 : 25
向 : 25
何处 : 24
问 : 24


