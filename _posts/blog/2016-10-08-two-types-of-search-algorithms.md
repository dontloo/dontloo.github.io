---
layout: post
title: "Two Types of Search Algorithms"
modified:
categories: blog
excerpt:
tags: []
date: 2016-10-08
modified: 2016-10-08
---

### Basics

There're two types of search algorithms, tree based and hash based.
Perhaps their simplest applications are [`tree maps`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) and [`hash maps`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html).

The performance of hash based search relies largely on the choice of hash functions, which are often to be designed carefully for different cases. Why not always use tree based search then? The limitation of tree based search is it requires the elements to be **comparable**.

### Approximate Nearest Neighbors
For search engines, we want a list of results most relavent to a given query, which can be modeled as the nearest neighbors of a given location according to some distance [metric](https://en.wikipedia.org/wiki/Metric_(mathematics)). In this setting it is assumed that the elements are comparable (otherwise there won't be the notion of "near" and "far"),  there are many smart tree based algorithms (kd tree, r\* tree, etc.) devised for nearest neighbor search. 

However exact search through large scale high dimensional data often takes more computations than people can afford, therefore, approximate nearest neighbor search (ANN) has come to the rescue. What ANN does is essentially trading off some accuracy in return for a (hopefully) huge speedup, and many ANN algorithms can be abstracted as the following two steps.

- Partition the space into many cells.
- Given a query, return the elements in its belonging cell (and adjacent cells).

In this case the running time of a query mainly depends on how its belonging cell (and adjacent cells) are partitioned and retrieved, which can be done in two ways, namely tree based and hash based.

For hash based partitions, the time complexity of getting the belonging cell of a query is constant w.r.t the number of cells \\(N\\). However the time complexity of getting the adjacent cells could be much higher depending on the choice of hash functions. There are many available options, such as locality sensitive hashing (LSH), k-means, hierarchical k-means, product quantization, which are not going to be discussed in this blog.

For tree based partitions, the running time of getting the belonging and adjacent cells can be bounded by \\(O(\log N)\\) with the use of priority queues. There's a very nice tree based algorithm named [ANNOY (Approximate Nearest Neighbors Oh Yeah)](https://erikbern.com/2015/10/01/nearest-neighbors-and-vector-models-part-2-how-to-search-in-high-dimensional-spaces/) that has basically every merit I ever wanted for an ANN algorithm, good job.
