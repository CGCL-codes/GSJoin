# GSJoin

Stream join is one of the most fundamental operations in data stream processing applications. Existing distributed stream join systems can support efficient two-way join, which is a join operation between two streams. Based the two-way join, implementing a multi-way join require to be split into double two-way joins, where the second two-way join needs to wait for the join result transmitted from the first two-way join. We show through experiments that such a design raises prohibitively high processing latency. To solve this problem, we propose GSJoin, a time-efficient multi-way distributed stream join system. We design a symmetric wait-free structure by symmetrically partitioning tuples and reused join. GSJoin utilizes reused join to join each new tuple with the intermediate result of the other two streams and stored tuples locally. For a new tuple, GSJoin only joins it with the intermediate result to generate the final result without waiting, greatly reducing the processing latency. Moreover, we design an intermediate data distribution structure based on dynamic attribute index graph to reduce the number of intermediate results and the system computing cost.

## How to use?

### Environment

We implement GSJoin on top of Apache Storm (version 1.2.3 or higher), and deploy the system on a cluster. Each machine is equipped with an octa-core 2.4GHz Xeon CPU, 64.0GB RAM, and a 1000Mbps Ethernet interface card. One machine in the cluster serves as the master node to host the Storm Nimbus. The other machines run Storm supervisors.

Build and run the example

```txt
mvn clean package

./storm jar ../target/GSjoin-1.0-SNAPSHOT.jar com.basic.core.Topology -n 90 -pr 45 -ps 45 -pt 45 -sf 8 -dp 8 -win -wl 2000 --remote --s random
```

-pr -ps  -pt: partitions of relation R S T

-sf -dp: instances of shuffle dispatcher

-win：enable sliding window

-wl：join window length in ms  

-ba: enable barrier  

--barrier-period: barrier period

--remote：run topology in cluster (remote mode)

--s: partion scheme


##Publication
If you want to know more detailed information, please refer to this paper:

Shuiying Yu, Yinting Zheng, Fan Zhang, Hanhua Chen, Hai Jin. TriJoin: A Time-Efficient and Scalable Three-Way Distributed Stream
Join System. Journal of Internet Technology, Vol. 24, No. 2, pp: 475-485, Mar. 2023

## Authors and Copyright

GSJoin is developed in National Engineering Research Center for Big Data Technology and System, Cluster and Grid Computing Lab, Services Computing Technology and System Lab, School of Computer Science and Technology, Huazhong University of Science and Technology, Wuhan, China by Shuiying Yu (shuiying@hust.edu.cn), Yinting Zheng(zhengyinting@hust.edu.cn), Fan Zhang(zhangf@hust.edu.cn), Hanhua Chen (chen@hust.edu.cn), Hai Jin (hjin@hust.edu.cn).

Copyright (C) 2021, [STCS & CGCL](http://grid.hust.edu.cn/) and [Huazhong University of Science and Technology](https://www.hust.edu.cn/).

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
  http://www.apache.org/licenses/LICENSE-2.0
```
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
