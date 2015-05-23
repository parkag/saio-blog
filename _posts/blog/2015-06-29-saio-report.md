---
layout: post
title: (Week  5) - SAIO performance
excerpt: ""
modified: 2015-06-29
categories: blog
tags: [SAIO, performance, report]
image:
  feature: random.jpg
comments: true
share: true
---

The goal of the first part of the project was to evaluate SAIO performance on a set of different queries and decide if the module could replace GEQO.

I have prepared a set of benchmarks for SAIO which consists of randomly generated queries with a configurable number of join relations. The outcome:

* [saio benchmarks repository](https://github.com/parkag/saio_benchmarks)
* [SAIO/GEQO report](/saio-blog/assets/files/GEQO_SAIO_report.pdf)

The conclusion is that in most of cases that I could find, GEQO is still the winner. SAIO definitely wins when optimizing queries with a lot of right joins, but not many seem to use these anyway.

This means that the Simulated Annealing algorithm behind SAIO is not strong enough to replace GEQO.

<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
