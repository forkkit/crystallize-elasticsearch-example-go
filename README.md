# Crystallize ElasticSearch Example

This repository is an example of how you might extend Crystallize to add search
functionality to your own tenant. The example provides shows how you can index
your tenant's catalogue within ElasticSearch, in bulk, and incrementally via
Crystallize webhooks.

This example was created using ElasticSearch 7.5 and was written in Go.

## Getting Started

### Prerequisites

- Go (with Go Modules enabled)
- Docker

### Installation

Clone the repository into your Go workspace.

```sh
git clone https://github.com/crystallizeapi/crystallize-elasticsearch-example
```

Install the required Go dependencies

```sh
go get
```

### ElasticSearch Cluster

Start the ElasticSearch cluster via docker-compose.

```sh
docker-compose up -d
```

## Running the Project

### Server

The server provides endpoints that can be used to create, remove, and update
indexes of individual items in the catalogue, as well as a search endpoint
that performs an aggregate query on the indexed data.

#### Running the Server

```sh
ES_NODE=YOUR_NODE_URL [ES_USER=YOUR_USER ES_PASS=YOUR_PASS] go run main.go
```

### Tasks

```sh
go run main.go -mode task -task <task-name>
```

#### `catalogue-bulk-index`

The catalogue-bulk-index task creates (or re-creates if it already exists) an
index within ElasticSearch for the catalogue. The task will perform a GraphQL
query to Crystallize's catalogue API to fetch all of the items, flatten the
results, and bulk index them within ElasticSearch.

```sh
go run main.go -mode task -task catalogue-bulk-index -tenant <tenant-identifier>
```
