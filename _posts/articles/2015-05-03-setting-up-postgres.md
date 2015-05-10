---
layout: post
title: Setting up Postgres with SAIO
excerpt: "Installation procedure on different systems"
modified: 2015-05-03
categories: articles
tags: [saio, postgres, setup]
image:
  feature: random.jpg
comments: true
share: true
---

Setting up Postgres with SAIO or GEQO turned on and off will be repeated multiple times during this project so it's worth being written down.

# Install process on Ubuntu:

## Quick install

{% highlight bash %}
sudo apt-get install postgresql
sudo apt-get install postgresql-client
{% endhighlight%}

## From source

{% highlight bash %}
doh
{% endhighlight%}

## Adding user

{% highlight bash %}
sudo su - postgres
createdb test_db
psql -s test_db
{% endhighlight%}

Now in the psql console:

{% highlight sql %}
CREATE USER greg PASSWORD 'greg';
GRANT ALL PRIVILEGES ON DATABASE test_db TO greg;
{% endhighlight%}

The database can be now accessed using the command:

{% highlight bash %}
psql postgresql://greg:greg@localhost:5432/test_db
{% endhighlight %}

[More stuff on this](https://wiki.postgresql.org/wiki/First_steps)

# Install SAIO

{% highlight bash %}
git clone https://github.com/parkag/saio.git
cd saio
make
sudo make install
{% endhighlight %}

Now, to enable SAIO in the psql console:

{% highlight sql %}
LOAD 'saio';
{% endhighlight %}

To disable SAIO:
{% highlight sql %}
SET saio TO 'false';
{% endhighlight %}

# Install process on Mac OS:

{% highlight bash %}
doh
{% endhighlight%}

TODO

# Install process on Windows:

TODO

<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
