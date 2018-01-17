# Logspout with Logstash adapter

Logspout with logspout-logstash installed. [Logspout-logstash](https://github.com/looplab/logspout-logstash) by looplab is a minimalistic adapter for github.com/gliderlabs/logspout to write to Logstash.

[![pipeline status](https://img.shields.io/docker/build/thojkooi/logspout.svg)](https://hub.docker.com/r/thojkooi/logspout/)


### Configuration options

The following environment variables for containers can be picked up on.

| Environment variable | Description |
|----------------------|-------------|
| `LOGSTASH_TAGS` | Comma seperated list of values added as `"tags"": ["value"]` for Logstash. Example: `-e LOGSTASH_TAGS="docker,production"` |
| `LOGSTASH_FIELDS` | Comma seperated list of additional fields added to the json output forwarded to Logstash. Example: `-e LOGSTASH_FIELDS="environment=production,example=helloworld"` |
| `DOCKER_LABELS` | Setting this to a non empty value will also forward all Docker labels to Logstash. |

See the readme on [looplap/logspout-logstash](https://github.com/looplab/logspout-logstash) for more information.

### Example compose file

```yml
version: '2'
services:
  logspout:
     image: thojkooi/logspout:v3.2.4
     restart: always
     volumes:
       - /var/run/docker.sock:/var/run/docker.sock
     environment:
       - ROUTE_URIS=logstash+tcp://logstash.localhost:5001
```
