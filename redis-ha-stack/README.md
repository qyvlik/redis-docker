# master-slave-with-failover

## startup one master and two slaves

There is three docker swarm node:

- swarm-master: manager
- swarm-worker-0: worker
- swarm-worker-1: worker

## get ip from swarm node

This docker stack use host mode, the docker swarm node ip is the redis server ip.

```bash
docker node inspect --format {{.Status.Addr}} swarm-master
```

## set label

Run the follow command on swarm-master.

```bash
docker node update --label-add redis-role=master swarm-master
```

## start up

Because the docker stack not support `.env` file, see [moby/moby/issues/29133](https://github.com/moby/moby/issues/29133), 
use the `export $(cat .env)`.

Run the follow commands on swarm-master.

```bash
export $(cat .env)
docker stack deploy -c redis-ha-stack.yml redis-ha-stack
```

### network



## stop

```bash
docker stack rm redis-ha-stack
```

# ref

- docker stack not support `.env`
- docker stack not support `network_mode`

[Docker Swarm概念与基本用法](https://note.qidong.name/2018/11/docker-swarm/)

[emmano3h/stackredis-ha](https://github.com/emmano3h/stackredis-ha)
