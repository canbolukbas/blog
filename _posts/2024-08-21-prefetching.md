---
title: "Prefetching"
date: 2024-08-21
---

This is the story of how I reduced N*M database queries to just one by prefetching.

I didn't figure out the performance problem, Sentry did. Sentry said there is a N+1 Query problem which was not quite correct. Yes, there were multiple similar queries. However it wasn't something to be solved with eager loading.

Problem: There are multiple database calls with the same query. Each db call takes under 10 ms, however they take total of 500 ms. It leads to... well... bad performance.

Let me simplify the problem. Imagine a two dimentional list. The outer list has N elements. The inner lists has up to M elements. Imagine you are iterating over this 2D list and performing same db query every single inner list item. It leads to N*M db calls.

```
for outer_item in outer_list:
    for inner_item in outer_item:
        data = query_database(inner_item)
        process_data(data)
```

Modeling the problem in a simpler way helped me identify the problem. I wrote the pseudocode of it and figured that prefetching the db table before iterating over this 2D list would only result with a single db call.

```
cached_data = prefetch_database_data()

for outer_item in outer_list:
    for inner_item in outer_item:
        data = cached_data.get(inner_item)
        process_data(data)
```
