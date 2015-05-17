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

Using fresh Ubuntu 14.04 installed on a virtual machine.

## Quick install

{% highlight bash %}
sudo apt-get install postgresql
sudo apt-get install postgresql-client
{% endhighlight%}

## From source

{% highlight bash %}
sudo apt-get install git
sudo apt-get install bison
sudo apt-get install flex
sudo apt-get install zlib1g-dev
git clone https://github.com/postgres/postgres.git
cd postgres
./configure
make
sudo su
make install
{% endhighlight%}

[More on this topic](http://www.postgresql.org/docs/9.4/interactive/installation.html) 

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

# Setting GUC variables
{% highlight sql %}
set saio_algorithm TO recalc; -- move/pivot/recalc
set saio_equilibrium_factor to 8; 
set saio_initial_temperature_factor to 2.0;
set saio_temperature_reduction_factor to 0.8;
set saio_moves_before_frozen to 2;
set saio_seed to 0.5;

set join_collapse_limit to 100;
set from_collapse_limit to 100;
{% endhighlight %}

# Install process on Mac OS:

{% highlight bash %}
NOT AVAILABLE YET
{% endhighlight%}

# Install process on Windows:

NOT AVAILABLE YET

<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
