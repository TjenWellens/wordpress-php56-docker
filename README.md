# WordPress on PHP-5.6 using docker

Running WordPress on PHP-5.6 with MySQL-5.7 on Docker container

## Motivation

- PHP for my site was updated to 7.2, but that broke my (long-time-not-updated) wordpress setup

## Prerequisites
1) Have an export of your db ; name the file `./wordpress.sql`
2) Have a copy of your entire wordpress installation ; put it in ./public_html/
3) Create an empty folder ./db_data
4) Create a file `./.env` (*1)
5) (optional) add line to sql (*2)
6) run
7) when all is running, change base url to `localhost:8080` (*3)

(*1) `.env` file should look something like this:
```
MYSQL_ROOT_PASSWORD=wordpress
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_PASSWORD=wordpress
```
(I filled in the actual values I used on the server)


(*2) My database could not load the ./wordpress.sql script. I needed to add the following line to the top of `./wordpress.sql`
```
SET SQL_MODE='ALLOW_INVALID_DATES';
```

(*3) Open phpmyadmin(http://localhost:8090/) and change in table `wp_options`
* home
* siteurl

to `localhost:8080` instead of `your-domain.com`

Or you can change the sql file for those entries:
```
# old
 INSERT INTO `wp_options` VALUES("1","siteurl","http://your-domain.com","yes");
# new
 INSERT INTO `wp_options` VALUES("1","siteurl","http://localhost:8080","yes");

# old
 INSERT INTO `wp_options` VALUES("37","home","http://your-domain.com","yes");
# new
 INSERT INTO `wp_options` VALUES("37","home","http://localhost:8080","yes");
```


## Running container
Building image
```sh
docker-compose build
```

Running containers:
```sh
docker-compose up
```

## Executing bash of wordpress container
```sh
docker-compose exec wordpress bash
```


## Stop services
`docker-compose down`


## Access the site:

http://localhost:8080/

## Access PhpMyAdmin

http://localhost:8090/

## Reference

- https://www.sitepoint.com/how-to-manually-build-docker-containers-for-wordpress/
- https://vsupalov.com/docker-arg-env-variable-guide/
