---
layout: page
title: About SAIO
excerpt: "SAIO is an alternative JOIN order optimizer for Postgres database"
modified: 2014-08-08T19:44:38.564948-04:00
image:
  feature: random.jpg
---

I'm **Grzegorz Parka**, software developer based in Warsaw (Poland) with academic background both in Applied Physics and Computer Science. I took part in Google Summer of Code 2014 where I developed Python library, [pykCSD](http://parkag.github.io/pykcsd-blog/), which is used mainly to analyze local electrical activity of packs of neurons.

For this summer I was chosen by the **Postgres** community to test and refine simulated annealing approach to optimize JOIN order for large queries. This is continuation of work made by Jan Urbański in 2010. During this summer I will work with SAIO - an alternative JOIN order optimizer, a possible replacement for old Genetic Query Optimizer (GEQO). The project is under the supervision of Atri Sharma.

**Simulated annealing** is a randomized metaheuristic for finding a global optimum in a large search space of an unknown shape. It is well suited for discrete search spaces, such as in case of JOIN ordering or the traveling salesman problem.

<figure>
    <img src="http://upload.wikimedia.org/wikipedia/commons/d/d5/Hill_Climbing_with_Simulated_Annealing.gif" width="100%">
    <figcaption>Hill climbing with simulated annealing -- wikipedia</figcaption>
</figure>

