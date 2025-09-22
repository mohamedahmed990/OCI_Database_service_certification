
Before you provision the capacity units, it is important to consider the following factors that impact the read, write, and storage capacities.

- **Record size**: As the record size increases, the number of capacity units consumed to write or read data also increases.
    
- **Data consistency**: Absolute consistency reads are twice the cost of eventual consistency reads.
    
- **Secondary Indexes**: In a table, when an existing record is modified (added, updated, or deleted), updating secondary indexes consume Write Units. The total provisioned throughput cost for a write operation is the sum of write units consumed by writing to the table and updating the local secondary indexes.
    
- **Data modeling choice**: With schema-less JSON, each document is self-describing which adds metadata overhead to the overall size of the record. With fixed schema tables, the overhead for each record is exactly 1 byte.
    
- **Query pattern**: The cost of a query operation depends on the number of rows retrieved, number of predicates, the size of the source data, projections, and the presence of indexes. The least expensive queries specify a shard key or index key (with an associated index) to allow the system to take advantage of primary and secondary indexes. An application can try different queries and examine the consumed throughput to help tune the operations.