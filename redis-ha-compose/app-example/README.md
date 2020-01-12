# defined your self app

## how to use

```js
let Redis = require("ioredis");
let redis = new Redis({
    sentinels: [
        {host: "redis-ha-compose_sentinel_1", port: 3000},
        {host: "redis-ha-compose_sentinel_2", port: 3000},
        {host: "redis-ha-compose_sentinel_3", port: 3000}
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

# ref

See [ioredis#sentinel](https://github.com/luin/ioredis/#sentinel)
