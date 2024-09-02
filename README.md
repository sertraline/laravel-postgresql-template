# How to start

dev-server: contains docker images and settings  
api: contains actual Laravel project

1. cd dev-server  
    * `cp .env.example .env`  
    * fill the .env variables    
2. Enter application directory: `cd api`  
    * `cp .env.example .env`  
    * fill the variables  
    * app key can be set with `base64:<b64 key you've generated>`  
3. Run containers: `docker compose up`  
4. Inside the same docker container, initialize composer:
    * `php composer-setup.php`
    * Install composer dependencies: `./composer.phar install`  
5. Run `php artisan optimize`


# Backups and maintenance
To back up the postgresql volume, run the following command:  
`docker run --rm --volumes-from laravelapp.psql-write -v $(pwd):/backup busybox tar cvf /backup/backup.tar /bitnami/postgresql`  

Then, to restore:  

```
sudo docker create -v /bitnami/postgresql --name DESTINATION busybox true
sudo docker run --rm --volumes-from DESTINATION -v $(pwd):/backup busybox tar xvf /backup/backup.tar
```

Check that the structure is correct:  

```
docker run --rm --volumes-from laravelapp.psql-write -v `pwd`:/back
up busybox ls /bitnami/postgresql
docker run --rm --volumes-from DESTINATION -v `pwd`:/back
up busybox ls /bitnami/postgresql
```
