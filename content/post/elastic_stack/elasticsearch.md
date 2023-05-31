---
title: "Elastic search"
date: 2023-05-31T13:23:17+05:30
draft: False
tags: ["elastic_stack"]
---

## Getting started

Please download the elasticsearch and kibana from below official websites for your OS.

[Elasticsearch](https://www.elastic.co/downloads/elasticsearch)

[Kibana](https://www.elastic.co/downloads/kibana)

I would be using Mac for elasticsearch and hence would provide those links for this purpose. 

[elasticsearch for Mac-Intel](https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.8.0-darwin-x86_64.tar.gz)

[Kibana for Mac-Intel](https://artifacts.elastic.co/downloads/kibana/kibana-8.8.0-darwin-x86_64.tar.gz)


## Local Installation Setup

Create a new directory and move those compressed files into the directory for extraction.

```
mkdir elastic-stack
tar -zxvf elasticsearch-8.8.0-darwin-x86_64.tar.gz
tar -zxvf kibana-8.8.0-darwin-x86_64.tar.gz
mv elasticsearch-8.8.0 elasticsearch
mv kibana-8.8.0 kibana
```

Open two terminals and move to respective directories for those two services. 

## Elasticsearch 

start the service, It provides the username, password and tokens as part of initial startup

```
cd elastic-stack/elasticsearch
bin/elasticsearch [ Enter ]

✅ Elasticsearch security features have been automatically configured!
✅ Authentication is enabled and cluster connections are encrypted.

ℹ️  Password for the elastic user (reset with `bin/elasticsearch-reset-password -u elastic`):
  Xl4mktLmPkO=22=_DwEl

ℹ️  HTTP CA certificate SHA-256 fingerprint:
  5c47f6c2bd182fc83cd9487af5dc400c3fa75013995fa8c5cf5b63c930803cb1

ℹ️  Configure Kibana to use this cluster:
• Run Kibana and click the configuration link in the terminal when Kibana starts.
• Copy the following enrollment token and paste it into Kibana in your browser (valid for the next 30 minutes):
  eyJ2ZXIiOiI4LjguMCIsImFkciI6WyIxOTIuMTY4LjAuMTA2OjkyMDAiXSwiZmdyIjoiNWM0N2Y2YzJiZDE4MmZjODNjZDk0ODdhZjVkYzQwMGMzZmE3NTAxMzk5NWZhOGM1Y2Y1YjYzYzkzMDgwM2NiMSIsImtleSI6ImlTd1BjSWdCRmJwS05TRUtLSmwyOm9sVlc2aEd1VG9tYVJVUThCZ2Y1c3cifQ==

ℹ️  Configure other nodes to join this cluster:
• On this node:
  ⁃ Create an enrollment token with `bin/elasticsearch-create-enrollment-token -s node`.
  ⁃ Uncomment the transport.host setting at the end of config/elasticsearch.yml.
  ⁃ Restart Elasticsearch.
• On other nodes:
  ⁃ Start Elasticsearch with `bin/elasticsearch --enrollment-token <token>`, using the enrollment token that you generated.
```

## Kibana

Start the service, after which they are prompted using the url to navigate into browser. 

```
xattr -d -r com.apple.quarantine kibana
cd elastic-stack/kibana
bin/kibana [ Enter ]

http://localhost:5200/_  ..

```


Provide the username and password generated from starting the elasticsearch cluster and use your own default dashboard for setup. 

If you want to query, then `hover` to the kibana dashboard -> `App ->dev_settings->console`

### search query using console

All the queries in the elasticsearch would be using an REST API under the hood when after successful validation would respond with an JSON object.

```
GET /_cluster/health  # Cluster health status
GET /_cat/indices?v # list indices
GET /_cat/nodes?v # list nodes 
```

### search query using curl

Since, its being an REST API call, you can use any of the client like `curl` or `postman` to query for the response. 

```
curl -H "Content-Type:application/json" --cacert config/certs/http_ca.crt -u elastic:Xl4mktLmPkO=22=_DwEl -X GET https://localhost:9200/products/_search -d '{"query": {"match_all":{}}}'
```

## Sharding

Data in Elasticsearch is organized into indices. Each index is made up of one or more shards. Each shard is an instance of a Lucene index, which you can think of as a self-contained search engine that indexes and handles queries for a subset of the data in an Elasticsearch cluster.

[Shard](https://www.elastic.co/blog/how-many-shards-should-i-have-in-my-elasticsearch-cluster)

## Replication

Each index is divided into shards and each shard can have multiple copies, and these are called as `replication group` and must always be kept in sync when docs are added and deleted. The copied shard from the replicatio group is called `replica shard` and for better fault tolerance they are kept in the secondary node. 

Note: In critical production, it would always be good to have a 3 nodes and incase if there are failures, we would be able to search data from other backups. 

## Snaphosts

A snapshot is a backup of a running Elasticsearch cluster. 

A snapshot copies segments from an index’s primary shards. When you start a snapshot, Elasticsearch immediately starts copying the segments of any available primary shards. If a shard is starting or relocating, Elasticsearch will wait for these processes to complete before copying the shard’s segments. If one or more primary shards aren’t available, the snapshot attempt fails

To back up an index, a snapshot makes a copy of the index’s segments and stores them in the snapshot repository.

## Adding additional nodes to the Elasticsearch

copy the tar file of the `elasticsearch` and place in a new directory and extract. 

```
mkdir elastic-stack/node2
cp elasticsearch-8.8.0-darwin-x86_64.tar.gz elastic-stack/second-node
tar -zxvf elasticsearch-8.8.0-darwin-x86_64.tar.gz 
mv elasticsearch-8.8.0 second-node
vim elastic-stack/second-node/node2/config/elasticsearch.yml

# modify the hostname, save & quit
node.name: second-node
```

Now, you need to get the active token from already running(master) elasticsearch. 

```
cd elastic-stack/elasticsearch/bin/
./elasticsearch-create-enrollment-token --scope node
```

copy the token and go to second node. 

```
cd elastic-stack/second-node/node2/
./bin/elasticsearch --enrollement-token <token>
```

Once they are joined, you would need to go to kibana dashboard console and query for the `GET /_cluster/health`
you would be seeing two nodes. 