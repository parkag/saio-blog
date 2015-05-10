---
layout: post
title: (Week  minus 3) - Playing with Postgres, benchmark ideas
excerpt: "Trying to find my own way to set up GEQO/SAIO benchmarks"
modified: 2015-05-10
categories: blog
tags: [introduction]
image:
  feature: random.jpg
comments: true
share: true
---


# Benchmark ideas

Looking for inspiration I came across an interesting presentation [Joining 1 million tables](http://www.slideshare.net/hansjurgenschonig/postgresql-joining-1-million-tables). It illustrates a similar approach that I want to take constructing part of my benchmarks.

I want my benchmarks to consist of two parts:

* Programatically generated schemas with configurable number of tables, fields and rows.

    Such schemas would not be particularly meaningful but would cover many general cases. This is some kind of a parametrized unit test.

* Schemas and queries that can be found in live real systems. 
    
    It seems that such queries are not very easy to find unless you have them in your own system :P


<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
