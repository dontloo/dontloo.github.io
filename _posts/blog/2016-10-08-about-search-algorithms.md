---
layout: post
title: "About Search Algorithms"
modified:
categories: blog
excerpt:
tags: []
date: 2016-10-08
modified: 2016-10-08
---

### Tree Based and Hash Based Search
Perhaps their simplest applications of tree based and hash based search are [`tree maps`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) and [`hash maps`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html).

The performance of hash based search relies largely on the choice of hash functions, which are often to be designed carefully for different cases. Why not always use tree based search then? The limitation of tree based search is it requires the elements to be **comparable**.

### Approximate Nearest Neighbors
For search engines, we want a list of results most relavent to a given query, which can be modeled as the nearest neighbors of a given location according to some (metric or non-metric) distance fucntion. In this setting it is assumed that the elements are comparable (otherwise there won't be the notion of "near" and "far"),  there are many smart tree based algorithms (kd tree, r\* tree, etc.) devised for nearest neighbor search. 

However exact search through large scale high dimensional data often takes more computations than people can afford, therefore, approximate nearest neighbor search (ANN) has come to the rescue. What ANN does is essentially trading off some accuracy in return for a (hopefully) huge speedup, and many ANN algorithms can be abstracted as the following two steps.

- Partition the space into many cells.
- Given a query, return the elements in its belonging cell (and adjacent cells).

In this case the running time of a query mainly depends on how its belonging cell (and adjacent cells) are partitioned and retrieved, which can be done in two ways, namely tree based and hash based.

For hash based partitions, the time complexity of getting the belonging cell of a query is constant w.r.t the number of cells \\(N\\). However the time complexity of getting the adjacent cells could be much higher depending on the characteristics of the hashing shcemes. There are many options available, such as (multiprobe) locality sensitive hashing (LSH), (hierarchical) k-means, product quantization, which are not going to be discussed in this blog.

For tree based partitions, the running time of getting the belonging and adjacent cells can be bounded by \\(O(\log N)\\) with the use of priority queues. There's a tree based algorithm [ANNOY (Approximate Nearest Neighbors Oh Yeah)](https://erikbern.com/2015/10/01/nearest-neighbors-and-vector-models-part-2-how-to-search-in-high-dimensional-spaces/) that has many nice properties, easy to extend the tree structure for incoming data, easy to switch between ANN and radius-based ANN queries, etc.

### Decentralized Graph Based Search for ANN
At the time of writing (2016), probably the best performing ANN algorithm is given by [NMSLIB](https://github.com/searchivarius/NMSLIB) based on based on hierarchical navigable small world graphs, which beats the best performing tree based (ANNOY) and hash based (FALCONN) algorithms considerably.

The algorithm represents elements as nodes in a small world graph. The core idea is analogous to routing algorithms, given a query, we first randomly select a node as a router, the router then select its closest neighbor to the query as the next router. The process is repeated until the closest neighbor to the query is the router itself, then the final router will be returned as the approximate nearest neighbor.

References:  
[Approximate nearest neighbor algorithm based on navigable small world graphs](https://www.hse.ru/pubs/share/direct/document/128296059)  
[Efficient and robust approximate nearest neighbor search using Hierarchical Navigable Small World graphs](https://arxiv.org/abs/1603.09320v1)
