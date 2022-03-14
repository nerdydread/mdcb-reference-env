MDCB Reference Environment
=================================
This project runs the Tyk OSS API Gateway in hybrid mode using the Tyk Pump to provide metrics for Prometheus.  Project includes containers for the Tyk Gateway, Tyk Pump, Redis, and Prometheus. This project as is, is intended to be connected to a pre-existing MDCB instance.


# Installation

Want to install using only Docker, or want a more advanced guide?  Visit the [Docker install](get-started/install-with-docker.md) page.

## Configuration - Hybrid Setup

If you are setting up a Hybrid cluster, do the following:

**NOTE:** If you are using Tyk Classic Cloud your `<MDCB-INGRESS>` url is: "hybrid.cloud.tyk.io:9091"

1. Change the following 3 values in `tyk.hybrid.conf`:
```json
    "slave_options": {
        "rpc_key": "<ORG_ID>",
        "api_key": "<API-KEY>",
        "connection_string": "<MDCB-INGRESS>:443",
```

it should look like this:

```json
    "slave_options": {
        "rpc_key": "j3jf8as9991ad881349",
        "api_key": "adk12k9d891j48df824",
        "connection_string": "persistent-bangalore-hyb.aws-usw2.cloud-ara.tyk.io:443",
```

2. Mount the hybrid conf into the Gateway in `docker-compose.yml`

From
```
- ./tyk.standalone.conf:/opt/tyk-gateway/tyk.conf
```

To:
```
- ./tyk.hybrid.conf:/opt/tyk-gateway/tyk.conf
```

That's it!  Now run `docker-compose up`

## Docker-Compose

With docker-compose, simply run 
```
$ docker-compose up -d
```

[1. Your First API](get-started/your-first-api.md)

[2. Your first token](get-started/your-first-token.md)

[3. Your First Plugin](get-started/your-first-plugin.md)

## To-Do

- Add Master DC componenents so project can be run locally without the need for an separate environment already running MDCB

