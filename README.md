# spread-server

Experiment to spread data over multiple machines


1. Start node with existing database, send query, get back sqlite database
2. Have client send database to node
3. Have node merge database
4. Have client shard database, send to N nodes, nodes verify and merge
5. 

* use nginx to deliver result files?
* client open connection, wait for result, finish request
* host will send command, make file, and return result


* how to asynch the request?
* what is the QoS?
* long tcp connection?
* requests session?
* request is pure sql, or soemthing else?
* tcp with json as request?



### Query

* Send query to server and get back response
* reduce latency of request
* Send query to master, master distrbutes query to many, and collects results
  * client send broadcast and reduce queries
  * 

### Ingestion

* rules for sharding data
  * simple hash-and-modulo
  * change number of shards? M nodes to extract N sub-shards for N new shards?
  * there is no simple module (or hard to find), so use a stack of rules to shard
  * can we scale from 1 to M shards with minimal movement?
  * [jump consistent hash](https://arxiv.org/ftp/arxiv/papers/1406/1406.2294.pdf) - uses random.next() for each rule, selecting 1/M each loop.
* Client will form database for submission
* Client will split database into shards and submit to each node
* Nodes will confirm sharding is correct

### Node startup

* bid on instances, start them
* Must have pointer to masters
* register self
* get shard info for each data cube
* query-only node must be notified when new files are on S3
* ingestion-shards must notify when new files are on S3


### Master Nodes

* Queries on the metadata cubes are run on all masters
* Node making request performs comparision for determining truth
* query balancing / resource balancing

  










## Alt tech:

https://www.pytables.org/