---
layout: post
title: "Batch vs Stream processing"
categories: "big-data-fundamentals"
---

Historically the two of them come from different use cases, but in the world of data lakes and warehouses the difference is getting smaller.  

**Batch processing** fits the need of "producing a report by reading large quantities of input data", like computing financial data over a year to get an annual report.  

**Stream processing** is better suited for "updating a report continuously by reading a small amount of data", like monitoring the amount of active users on a website. 
 

![Batch vs Stream](/assets/img/batch-stream.png)
 
   

Interestingly, if we stick with these examples, we can actually imagine computing a financial report continuously as new transactions come in. We would then have our annual report updated "live". Could stream processing be a one-size-fits-all solution?  

Unfortunately it is not that easy.  

The issue arise from what needs to be computed to update the report. If updating the report just requires to add a transaction, then the calculations is probably adding the value of the transaction to the previous totals.  

However if the update is about modifying an existing transaction, then we need more information and more computing: fetching the previous transaction and computing the difference for the totals. And this is something that may be complex to program. Furthermore most stream processing engines use a "state" to keep in-memory what may have to be updated, the size of this state will define the capabilities of the processing.  

Whereas doing so in batch processing is much more easier: the full information is read and computed anyway, even if that requires more time and resources.  

## Summary:
### Batch:
- Computes large inputs of data at a time
- Easier to program

### Stream:
- Computes only the latest data at a time
- Can be more complex to program, especially to manage state size

## End notes:
- Batch processing may hit the same limitations as stream processing, in so-called "incremental materialization". When computing the whole history is not even possible with a batch engine, and only the latest date/week can fit in memory.

- In the modern data warehouses, SQL is the preferred language for batch processing. Even though some technologies offer a SQL API for stream processing, it may show limitations to manage the issues mentioned here. Depending on the technology and your use cases, the capabilities may vary.
[RisingWave](https://github.com/risingwavelabs/risingwave) and [Materialize](https://github.com/MaterializeInc/materialize) are capable of managing arbitrary large state sizes, which makes them ideal SQL-stream-processing engines. However they are quite new and not production-grade.

- In the world of finance, modifications are only allowed for a given period. By preventing the incursion of "late arriving data", the state size can be constrained to an acceptable size. If you can, pushing that constraint to your data sources/producers will reveal useful for stream processing.