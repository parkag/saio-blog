---
layout: post
title: (Week 1) - Small improvements in SAIO repo
excerpt: ""
modified: 2015-05-25
categories: blog
tags: [introduction]
image:
  feature: random.jpg
comments: true
share: true
---

This week I did some small improvements to prepare the environment for the further development.

##Setting Continuous intergration server for SAIO

I updated the tests and decided that there should be a continuous integration server to improve developer's comfort.
The project is developed on Github so the natural choice is Travis-CI.
I found out that there already are established routines for testing PGXN modules. Thanks to the [blog post](http://petereisentraut.blogspot.com/2013/07/testing-postgresql-extensions-on-travis.html) one of core PostgreSQL developers, Peter Eisentraut I could set up Travis pretty quickly.

##Correcting tests

The unit tests provided with SAIO were failling. They were not updated after removing SAIO alternative algorithms. They were still trying to set saio_algorithm = pivot or move long after they were removed from the source code.

## Further actions ideas

###Correcting package layout

I want to enable using ```CREATE EXTENSION``` command.
Also standarization of such library seems good.

### Enable test coverage report

It is possible to generate code coverage reports from PostgreSQL code. It would be very useful to have this information available on SAIO as well.


##Queries with several join relations

There is no point to write these queries by hand unless one has a great idea of exposing something strange. For a general purpose benchmark I will create a set of python scripts which will create different queries and schemas programmatically and run SAIO/GEQO comparison tests on them.

<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
