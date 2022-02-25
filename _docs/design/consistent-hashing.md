---
title: "Consistent Hashing"
layout: blog
order: 1
topic: System Design
topic_path: /docs/design/index.html
---
*Notes from [System Design Interview.](https://www.amazon.com/System-Design-Interview-insiders-Second/dp/B08CMF2CQF/ref=sr_1_1?keywords=system+design+interview&qid=1645591606&sprefix=system+desi%2Caps%2C166&sr=8-1)*

Horizontal scaling adds more compute by adding more machines to the resource pool, rather than increasing the hardware on existing machines. Ideally, load will be distributed evenly. Consistent hashing is a technique which can be used to balance a load across the machines in the resource pool.

## Rehashing
One solution involves using a simple hash function to distribute requests across the number of machines in the resource pool. If we have `n` machines, and data with a `key`, we can use the following function to assign the data to a machine.

```python
server = hash(key) % n
```

The rehashing problem arises when a server goes offline. When the size of the resource pool `n` changes, the hash function will map existing data to the wrong servers.

## Hash Rings
The hash function defines a hash space. In the case of the modulus function above, the hash space is size `n`. Let's take the linear hash space and form a ring.

<img src="{{ site.baseurl }}/assets/img/docs/design/hash-ring.png" alt="Hash Ring">

Data is mapped to the next server encountered when traveling clockwise around the ring. In the picture above, Bill's data is stored on server A, Jane and Kate's is stored on server C, and John and Steve's is stored on server B.

When a new server is added or removed from the server pool, only a small amount of data needs to be remapped. However, one problem becomes distributing the data evenly between servers. If a server is added, the partitions will not be of equal size.

Virtual nodes solve this problem - we can add more than one node for a single server onto the hash ring. In this way we can distribute data evenly across the resource pool.