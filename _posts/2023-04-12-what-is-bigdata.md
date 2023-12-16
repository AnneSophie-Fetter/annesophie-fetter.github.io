---
layout: post
title: "What is Big Data?"
categories: "Big Data Fundamentals"
---


Big Data is a term used quite a lot in the media to describe "large amounts of data".  
But this begs the question:  
How big should the data be to qualify as Big Data™, terabytes, petabytes?  

Counter-intuitively, Big Data is not so much about data, than it is about the technologies used to store and process it.  

The data becomes "big" when you are pushed to change __not only__ the system, but also the way your system scales with data.

![Vertical vs Horizontal Scaling](/assets/vertical-horizontal-scaling.png)

## Vertical scaling

A simple approach to scaling would be "vertical scaling": upgrading an existing machine, by adding disk space, replacing the CPU, or the motherboard.  
This increases the price significantly, and not in a linear way: equipment twice as performant can cost up to four times as much (and more for high-end equipment).

## Horizontal Scaling

Instead of buying more expensive equipment, one can buy multiple instances of a relatively cheap machine and just organize them to handle the data.
Coordination of multiple instances ("nodes") will require specialized software, which belongs to the "distributed systems" family. This is where you will find names such as Hadoop, Spark or Kafka. These can handle arbitrarily high volumes of data. Hence the name "Big Data".

They offer additional perks:
- Fault tolerance: Service continues if a node crashes, without loss of data
- Elasticity: Add/Remove nodes without disruption

## Summary
__Big Data:__
- Is more about the technology than the volume of data
- Comes from the "horizontal scaling" strategy
- Requires software which coordinates multiple nodes to handle data
- Enables features such as Fault Tolerance and Elasticity

__End Notes:__
- With the democratization of cloud services, the difference between vertical and horizontal scaling is blurred: cloud providers make extensive use of virtualisation. Therefore the considerations about number of machines becomes obsolete. Check out their documentation to understand how they scale.
- Even though horizontal scaling seems like a rational choice if you expect a need to scale, using "Big Data" software is not trivial and requires engineers to install and operate complex systems. Consequently, companies should factor-in that added cost.
