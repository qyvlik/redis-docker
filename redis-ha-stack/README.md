# master-slave-with-failover

There is three docker swarm nodes:

- swarm-master: manager
- swarm-worker-0: worker
- swarm-worker-1: worker

## get ip from swarm node

This docker stack use **host** network mode, the docker swarm nodes ip is the redis servers ip.

So you can connect the redis servers by use the IDE, such as IntelliJ IDEA.

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

### how to use

Use node js, see [ioredis#sentinel](https://github.com/luin/ioredis/#sentinel).

```ecmascript 6
let Redis = require("ioredis");
let redis = new Redis({
    sentinels: [
        // please use the `docker node inspect --format {{.Status.Addr}} swarm-master` to get ip
        {host: "IP_OF_swarm-master", port: 3000},
        {host: "IP_OF_swarm-worker-0", port: 3000},
        {host: "IP_OF_swarm-worker-1", port: 3000}
    ],
    name: "master-node"
});
(async () => {
    let key = "foo";
    let rawValue = Date.now();
    await redis.set(key, rawValue + "");
    let value = await redis.get(key);
    console.info(`get key:${key}, value:${value}`);
})();
```

## stop

```bash
docker stack rm redis-ha-stack
```

# ref

- docker stack not support `.env`
- docker stack not support `network_mode`

[Docker Swarm概念与基本用法](https://note.qidong.name/2018/11/docker-swarm/)

[emmano3h/stackredis-ha](https://github.com/emmano3h/stackredis-ha)
