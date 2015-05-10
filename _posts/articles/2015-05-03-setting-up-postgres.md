---
layout: post
title: Setting up Postgres with SAIO
excerpt: "Installation procedure"
modified: 2015-05-03
categories: articles
tags: [saio, postgres, setup]
image:
  feature: random.jpg
comments: true
share: true
---

Setting up Postgres with SAIO or GEQO turned on and off will be repeated multiple times so it's worth being written down.

# Install process on Ubuntu:

## Quick install

```
sudo apt-get install postgresql
sudo apt-get install postgresql-client
```

## From source

```
doh
```

## Adding user

```
sudo su - postgres
createdb test_db
psql -s test_db
```

Now in the psql console:

```
CREATE USER greg PASSWORD 'greg';
GRANT ALL PRIVILEGES ON DATABASE test_db TO greg;
```


# Install process on MacOS:

```
doh
```

//TODO



<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
