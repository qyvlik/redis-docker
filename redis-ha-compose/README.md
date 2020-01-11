# master-slave-without-failover

## startup one master and two slaves

```bash
docker-compose up --scale slave=2 --scale sentinel=2 -d
```

---

[Redis集群之主从复制，读写分离（上）（五）](https://blog.csdn.net/cuipeng0916/article/details/53704629)
