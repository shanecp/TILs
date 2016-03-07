## Docker Commands

### View all dangling volumes
```
docker volume ls --filter dangling=true
```

### Remove all dangling volumes
```
docker volume rm $(docker volume ls -qf dangling=true)
```
