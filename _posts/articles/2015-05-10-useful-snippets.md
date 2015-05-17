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

## Drop all tables from a schema as a non-privileged user

{% highlight sql %}
select 'drop table if exists "' || tablename || '" cascade;' 
  from pg_tables
 where schemaname = 'public';
{% endhighlight %}


# Other useful commands
Finding the Postgres configuration file

{% highlight bash %}
sudo updatedb
locate postgresql.conf
{% endhighlight %}

Example output

{% highlight bash %}
/etc/postgresql/9.3/main/postgresql.conf
{% endhighlight %}

Generating Postgres schema diagram on Ubuntu

{% highlight bash %}
sudo apt-get install postgresql-autodoc
postgresql_autodoc -t dot -h localhost -u greg -d database_name --password
dot -Tpng database_name.dot -o diagram.png
{% endhighlight %}


<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
