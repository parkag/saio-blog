---
layout: post
title: Initial state of SAIO
excerpt: "What this project begins with"
modified: 2015-05-17
categories: articles
tags: [postgres, saio ]
image:
  feature: random.jpg
comments: true
share: true
---

Jan Urbański prototyped the SAIO module. I [forked](https://github.com/parkag/saio) it to continue his work. Here I will briefly describe what is in the repository.

##doc

This directory contains readme file with:

* [GUC](http://www.enterprisedb.com/postgres-plus-edb-blog/bruce-momjian/what-guc-variable) variables defined by the module with brief explanation (SAIO parameters that can be set during runtime or in conf file).
[More on GUC in general](http://www.slideshare.net/PGExperts/guc-tutorial-package-90)
* a warning that the module is not production ready.

##pgcon2010

Presentation from PGCon2010 which contains overview of SAIO module and some background information. Interesting read. Also a must-read for someone entering the project.

The most interesting parts:

* explanation of algorithms for moving in the solution space
    - move
    - pivot
    - recalc

The presentation can be also viewed [here](https://www.pgcon.org/2010/schedule/attachments/150_saio.pdf).

##queries

SQL queries used to test SAIO performance and correctness. It contains:

### complex.sql and explain.sql

Both files contain the same query with 13 JOIN relations, described as a *moderately complex query*. There are references for this query in the PGCon2010 presentation.

Complex sql has default explain format, explain.sql uses explain format xml.

### dump.sql

A more complex schema to test queries with foreign key constraints (?).

<figure>
    <a href="{{ site.url }}/images/dumpsql.png">
    <img src="{{ site.url }}/images/dumpsql.png" alt="schema diagram from dump.sql">
    </a>
    <figcaption>Schema diagram of dump.sql.</figcaption>
</figure>

### obvious.sql

Sets some specific saio parameters and performs a small query (3 joins).

### query.sql

5 JOINS

### robert.sql

Setting SAIO parameters for bigger queries (join_collapse_limit = 100, from_collapse_limit = 100)

### saio-start.sql

Setting some common SAIO parameters.

### schema.sql and view.sql

<figure>
    <a href="{{site.url}}/images/schemasql.png">
    <img src="{{site.url}}/images/schemasql.png" alt="schema diagram from dump.sql">
    </a>
    <figcaption>Schema diagram of schema.sql.</figcaption>
</figure>

view.sql creates views that contain queries:

* information_generic_allowance: 2 JOINS + 12 LEFT JOINS (with subqueries)
* information_genetic_allowance: 2 JOINS + 21 LEFT JOINS (with subqueries)
* information_patient_diagnosis: 24 JOINS + 9 LEFT JOINS (with subqueries)
* information_patient_placeholder: 18 JOINS + 11 LEFT JOINS (with subquries)
* information_sample_placeholder: 11 JOINS + 18 LEFT JOINS (with subqueries)

### star.py

Python script generating a sql script for simple [star schema](http://en.wikipedia.org/wiki/Star_schema) with one central table and N arms.

Example usage:
{% highlight bash %}
python star.py 5
{% endhighlight %}

Generates:

{% highlight sql %}
drop table if exists center;
create table center (col0 int, col1 int, col2 int, col3 int, col4 int);
drop table if exists arm0; create table arm0 (col int);
drop table if exists arm1; create table arm1 (col int);
drop table if exists arm2; create table arm2 (col int);
drop table if exists arm3; create table arm3 (col int);
drop table if exists arm4; create table arm4 (col int);
insert into arm0 (select generate_series(1, 10000));
insert into arm1 (select generate_series(1, 10000));
insert into arm2 (select generate_series(1, 10000));
insert into arm3 (select generate_series(1, 10000));
insert into arm4 (select generate_series(1, 10000));
insert into center(col0, col1, col2, col3, col4) values (0, 1, 2, 3, 4);
analyze;
explain select * from arm0, arm1, center, arm2, arm3, arm4 where arm0.col = col0 and arm1.col = col1 and arm2.col = col2 and arm3.col = col3 and arm4.col = col4;
{% endhighlight %}

##test

Contains tests in similar format as Postgres regression tests. Content:

* schedule - a file that defines which tests are run, test names correspond to file names in *sql* and *expected* directories.
* sql - contains 4 files with example input sql scripts for tests
* expected - contains 4 files with expected output of tests

They can be run via the Makefile
{% highlight bash %}
make install
make installcheck
{% endhighlight %}
I saw that the tests are failling on [PGXN tester](http://www.fuzzy.cz/tmp/pgxn-tester/#). However didn't manage to run them locally yet for some reason.


##scripts
SAIO testing scripts and other utilities.

###analyse-results.py
//TODO

###check-speed.py
Script that measures execution time of provided queries for different SAIO parameters or using GEQO if no parameters provided.

Usage:
{% highlight bash %}
python check-speed.py --loops 100 --timeout 50 --query1 testing_query.sql --query2 testing_query2.sql
{% endhighlight %}


###compile-dot
Transforms .dot files (output from oprofiler?) to .png images.

###oprofile-start and oprofile-stop
Scripts for managing [oprofile](http://lbrandy.com/blog/2008/11/oprofile-profiling-in-linux-for-fun-and-profit/) profiller. Small oprofile tutorial [here](http://ssvb.github.io/2011/08/23/yet-another-oprofile-tutorial.html).

###psql-gdb
Script that attaches gdb to Postgres backend.


##src

Luckily the code is quite well commented! Thanks Jan! :)
However maybe it can be made a little more self explanatory.

###saio_main.c
Manages connection with postgres optimizer (loading and unloading join_search_hook), defines GUC variables, calls simulated annealing algorithm.

###saio.c and saio.h
saio.h contains structures definitions

saio.c contains state managing functions and implementation of simulated annealing algorithm.

###saio_debug.c and saio_debug.h
Functions for printing saio state and query trees.

###saio_trees.c and saio_trees.h
Define operations on Query trees.

###saio_util.c and saio_util.h
Managing random numbers, evaluating joins.
I don't yet understand the *join_can_be_legal()* function.
//TODO

###saio_recalc.c
//TODO

###saio_probes.h
Defines tracing procedures. (For debugging purposes?)
//TODO

###saio_probes.d
I don't understand this one yet.

###Gen_dummy_probes.sed
I don't understand this one yet.


#PGXN

The module is available on PGXN as an extension. [More info about creating PGXN packages.](http://manager.pgxn.org/howto)


#How it interacts with Postgres - HOOK

SAIO module is communicating with PostgreSQL through a [hook](https://wiki.postgresql.org/images/e/e3/Hooks_in_postgresql.pdf), more precisely join_search_hook.

#Why SAIO is bad now

I don't agree with the author that the code is particularly ugly. It can be made a bit more self explanatory but other than that it looks fine.

The module surely can be tested more extensively. Small updates may be useful 
to conform better to the PGXN layout or the /contrib layout.

//TODO find the bad parts, compare with some newer contrib modules

<figure>
    <img src="{{ site.url }}/images/gsoc_horizontal.jpg" width="100%">
</figure>
