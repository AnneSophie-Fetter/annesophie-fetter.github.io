---
layout: post
title: "Lambda vs Kappa architecture"
categories: "big-data-fundamentals"
---



When BigData analytics need to be both accurate and low-latency, we need to combine batch and stream processing in our data warehouse.

## Lambda:

The historical way to dive into low-latency given a Data Lake or a Data Warehouse was to add another layer to the existing batch processing. That additional layer would use a different engine, made for stream processing.
Both of them would compute the data with the same business logic, but would not apply the same way:  

- Stream Layer: computes only the latest data received
- Batch Layer: computes historical data, or late arriving data.  
In general it enables recomputing the existing datasets when a change occurs - operation also known as “backfilling”.


Both of these layers write to the same “serving” layer, which contains the data queried by the users.  

   

![Lambda](/assets/img/lambda.png)

   

However the biggest drawback of this architecture is that the same business logic is written twice, for different engines, and possibly in different programming langues.  
This requires two sets of skills in the team, increasing complexity and thus decreasing its maintainability.

## Kappa:

It is a suggestion to solve the challenges of the lambda architecture: why not use only the stream layer?

Indeed, whatever the batch layer does, the stream layer could do as well: backfilling could be done by re-emitting data, and recomputing it in the stream layer.

   

![Kappa](/assets/img/kappa.png)

   

This, of course, incurs some challenges:

- *Low-Latency vs High-Throughput*: The streaming engine, specialized in low-latency, may struggle to handle a batch of data, as it needs to be tuned for high-throughput.
- *Disruption of the live data*: If the re-emitted data is on the same lane, then we are competing the backfill processing against the stream processing which usually needs to have priority.

This implies a dedicated toolset to be able to handle the “batch” aspect of data platform operations. It may carry its own amount of complexity.


## Summary:

### Batch:

- Dedicated stream layer next to the batch layer
- Complexity incurred by having two sets of processing layers with the same logic written twice.

### Stream:

- Single stream layer that handles both use-cases
- Backfilling becomes a challenge and requires dedicated tooling to do it properly

   

***  

   

### End note:

Even though both of these architecture are presented as equivalent and having trade-offs, historically lambda came first, and kappa was a proposed alternative that showed its limitations. Databricks proposed yet another alternative that seems to be a compromise between the two: the delta architecture: using the same engine (and potentially the same code), to do both stream and batch processing separately. As a lot of the ease of use comes from proprietary tooling, it would be prudent to not brand it as a standard architecture.