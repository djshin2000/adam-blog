---
layout: post
title:  (Sample) I meet the sunset
date:   2017-08-24 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: post-2.jpg # Add image post (optional)
tags: [Blog, Sunset]
author: # Add name author (optional)
---
큰 제목입니다.
==========
```
pip install django
```

{% highlight Python %}
def document_form_thumbnail_path(instance, filename):
    title = instance.title
    fn, ext = os.path.splitext(filename)
    datetime = datetime.now()
    re_filename = datetime.strftime('%Y%m%d_%H%M%S_') + title + 'thumbnail' + ext
    paths = ['document', 'document-form', re_filename]
    return os.path.join(paths)
{% endhighlight %}

```python
def document_form_thumbnail_path(instance, filename):
    title = instance.title
    fn, ext = os.path.splitext(filename)
    datetime = datetime.now()
    re_filename = datetime.strftime('%Y%m%d_%H%M%S_') + title + 'thumbnail' + ext
    paths = ['document', 'document-form', re_filename]
    return os.path.join(*paths)
```

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}
