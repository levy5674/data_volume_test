# Data Volume Test
---
Playpen for showing how two docker containers can share data.

`docker-compose.yml` creates two containers running ubuntu, and shares a data
dir between them


## Starting containers

```{bash}
docker-compose up
Starting datavolumetest_writer_1...
Starting datavolumetest_reader_1...
```

## Connect to writer, and write

```{bash}
docker exec -it datavolumetest_writer_1 bash
echo "Hello" >> /data/hello
exit
```

## Connect to reader and read

```{bash}
docker exec -it datavolumetest_reader_1 bash
cat /data/hello
exit
```

---
**NOTE** docker-compose 1.4.1 does not allow `volumes_from` to specify the
readonly flag.  When 1.5.0 is part of the mac toolbox we can change

```
volumes_from:
    - 'writer'
```

to

```
volumes_from:
    - 'writer:ro'
```

to get the desired effect.
