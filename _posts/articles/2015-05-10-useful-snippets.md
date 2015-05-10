---
layout: post
title: Useful code snippets
excerpt: "semi-random stuff"
modified: 2015-05-10
categories: articles
tags: [sql, postgres ]
image:
  feature: random.jpg
comments: true
share: true
---


## What tables do I have in my schema

{% highlight sql %}
SELECT tablename FROM pg_tables WHERE schemaname = 'public';
{% endhighlight %}



# Other useful commands
Finding the conf file

{% highlight bash %}
sudo updatedb
locate postgresql.conf
{% endhighlight %}

Example output

{% highlight bash %}
/etc/postgresql/9.3/main/postgresql.conf
{% endhighlight %}

<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
