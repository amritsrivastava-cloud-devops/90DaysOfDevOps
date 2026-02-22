## Installation of mysql on docker 

```
docker run -d --name mysql-TWS -e MYSQL_ROOT_PASSWORD=12345 mysql
docker exec -it id bash
mysql -u root -p
```

## Installation of mongodb on docker 

```
docker run -d mongo
docker exec -it id bash
mongosh
```
