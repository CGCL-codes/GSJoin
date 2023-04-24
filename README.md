# GSJoin

Stream join is one of the most fundamental operations in data stream processing applications. Existing distributed stream join systems can support efficient two-way join, which is a join operation between two streams. Based the two-way join, implementing a multi-way join require to be split into double two-way joins, where the second two-way join needs to wait for the join result transmitted from the first two-way join. We show through experiments that such a design raises prohibitively high processing latency. To solve this problem, we propose GSJoin, a time-efficient multi-way distributed stream join system. We design a symmetric wait-free structure by symmetrically partitioning tuples and reused join. GSJoin utilizes reused join to join each new tuple with the intermediate result of the other two streams and stored tuples locally. For a new tuple, GSJoin only joins it with the intermediate result to generate the final result without waiting, greatly reducing the processing latency. Moreover, we design an intermediate data distribution structure based on dynamic attribute index graph to reduce the number of intermediate results and the system computing cost.

## How to use?

### Environment

We implement Simois atop Apache Storm (version 1.2.3 or higher), and deploy the system on a cluster. Each machine is equipped with an octa-core 2.4GHz Xeon CPU, 64.0GB RAM, and a 1000Mbps Ethernet interface card. One machine in the cluster serves as the master node to host the Storm Nimbus. The other machines run Storm supervisors.

Build and run the example

```txt
mvn clean package

./storm jar ../target/Trijoin-1.0-SNAPSHOT.jar com.basic.core.Topology -n 90 -pr 45 -ps 45 -pt 45 -sf 8 -dp 8 -win -wl 2000 --remote --s random
```

-pr -ps  -pt: partitions of relation R S T

-sf -dp: instances of shuffle dispatcher

-win：enable sliding window

-wl：join window length in ms  

-ba: enable barrier  

--barrier-period: barrier period

--remote：run topology in cluster (remote mode)

--s: partion scheme

