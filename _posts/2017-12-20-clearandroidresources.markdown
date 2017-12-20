---
layout: post
title:  "Clean no use android strings"
date:   2017-12-18 14:31:25 +0800
categories: android
---
Android Apps UI will change largely,there will be many no use strings in android resources.
And some Apps may support many languages(locales), for example, our App support nearly 60 locales.
So removing no use strings in each locale is a lot of work. So....

{% highlight python %}

from xml.etree.ElementTree import ElementTree, Element 
import os 
#parse string to be removed
with open("~/data/strings_removed.txt") as txt:
    strings_removed = txt.readlines()

#print(strings_removed)
strings_removed_stip = []
for string in strings_removed:
    strings_removed_stip.append(string.strip())

#print(strings_removed_stip)
#parse string

paths = "~/data/temp/"
for (dirpath, dirnames, _) in os.walk(paths):
    if(dirpath == paths):
        continue
    #print(dirnames)

    file_path_name = dirpath + "/" + "strings.xml"
    if os.path.isfile(file_path_name):
        xmlTree = ElementTree()
        xmlTree.parse(source=file_path_name)  #读入  
        root = xmlTree.getroot()
        for string in root.findall('string'):
            for str_remove in strings_removed_stip:
                name = string.attrib['name']
                if name == str_remove:
                    #print(name)
                    root.remove(string)#remove no use string node
        #add namespace            
        root.set("xmlns:android", "http://schemas.android.com/apk/res/android")
        root.set("xmlns:xliff", "urn:oasis:names:tc:xliff:document:1.2")
        #write back to file
        xmlTree.write(file_path_name, 'utf-8', False);

{% endhighlight %}
