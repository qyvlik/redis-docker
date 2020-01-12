# master-slave-with-failover

## startup one master and two slaves

```bash
docker-compose up --scale redis-slave=2 --scale sentinel=3 -d
```

- `redis-slave`: redis slave server node
- `sentinel`: redis sentinel server node

## hostname

The container hostname format is `${docker_compose_project_name}_${container_name}_${scale_index}`

- `redis-master`: redis-ha-compose_redis-master_1
- `redis-slave`: 
    - redis-ha-compose_redis-slave_1
    - redis-ha-compose_redis-slave_2
    - redis-ha-compose_redis-slave_N
- `sentinel`: 
    - redis-ha-compose_sentinel_1
    - redis-ha-compose_sentinel_2
    - redis-ha-compose_sentinel_3
    - redis-ha-compose_sentinel_N

## defined your self app

See [app-example](./app-example), and the follow env:

- `REDIS_HA_COMPOSE_APP_EXTENDS_FILE`: your self app docker-compose.yml file
- `REDIS_HA_COMPOSE_APP_EXTENDS_SERVICE`: your self app service name in docker-compose.yml file

---

[Redis集群之主从复制，读写分离（上）（五）](https://blog.csdn.net/cuipeng0916/article/details/53704629)
