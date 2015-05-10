---
layout: post
title: Useful code snippets
excerpt: "Installation procedure"
modified: 2015-05-10
categories: articles
tags: [sql, postgres ]
image:
  feature: random.jpg
comments: true
share: true
---


## How many tables do I have in my schema

```sql
SELECT count(tablename) FROM pg_tables WHERE schemaname = 'public';
```





# Other useful commands
Finding the conf file

```shell
sudo updatedb
locale postgresql.conf
```

Example output

```shell
/etc/postgresql/9.1/main/postgresql.conf
```


<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
