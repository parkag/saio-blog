---
layout: page
title: About me and the project
excerpt: "SAIO is an alternative JOIN order optimizer for Postgres database"
modified: 2015-05-03T19:44:38.564948-04:00
image:
  feature: Warsaw_Central_Station_by_night.jpg
---

I'm **Grzegorz Parka**, software developer based in Warsaw (Poland) with academic background both in Applied Physics and Computer Science. I took part in Google Summer of Code 2014 where I developed Python library, [pykCSD](http://parkag.github.io/pykcsd-blog/), which is used mainly to analyze local electrical activity of groups of neurons. This year I participate in [**Google Summer of Code 2015**](http://www.google-melange.com/gsoc/homepage/google/gsoc2015).

For this summer I was chosen by the **Postgres** community to test and refine simulated annealing approach to optimize JOIN order for large queries. During this summer I will work with [SAIO](https://github.com/wulczer/saio) - an alternative JOIN order optimizer, a possible replacement for old [Genetic Query Optimizer (GEQO)](http://www.postgresql.org/docs/9.4/static/geqo.html). This is continuation of work made by Jan Urbański in 2010. The project is under the supervision of Atri Sharma.

**Simulated annealing** is a randomized metaheuristic for finding a global optimum in a large search space of an unknown shape. It is well suited for discrete search spaces, such as in case of JOIN ordering or the traveling salesman problem.

<figure>
    <img src="http://upload.wikimedia.org/wikipedia/commons/d/d5/Hill_Climbing_with_Simulated_Annealing.gif" width="100%">
    <figcaption>Hill climbing with simulated annealing -- wikipedia</figcaption>
</figure>

