# iTranswarp

Full-featured CMS including blog, wiki, discussion, etc. powered by SpringBoot.

[![Build Status](https://travis-ci.org/michaelliao/itranswarp.svg?branch=master)](https://travis-ci.org/michaelliao/itranswarp)

* based on SpringBoot 2.x
* OAuth2 integration (weibo, QQ, facebook, etc.)
* SEO support
* REST API
* customized css with uikit2

### Environment

- JDK 11
- MySQL 5.7
- Redis 4/5
- Nginx

### Build

```
$ mvn -DskipTests=true clean package
```

Or check [build.sh](blob/master/build.sh).

### Initialize database

DDL and test data are generated by [SchemaBuilder.java](blob/master/src/main/java/com/itranswarp/SchemaBuilder.java).

Create schema:

```
$ mysql -u root -p < release/ddl.sql
```

NOTE: re-run this SQL file will remove all existing data.

Import test data:

```
$ mysql -u root -p it < release/init.sql
```

### Run
 
```
java -jar itranswarp.jar
```

### Configuration

All configurations are passed by environments:

```
$ PROFILES=production TIME_ZONE=Asia/Shanghai DOMAIN=example.com \
  DB_HOST=localhost DB_PASSWORD=changeit \
  REDIS_HOST=localhost \
  java -jar itranswarp.jar
```

Please check [application.yml](blob/master/src/main/resources/application.yml) for environment variables.

### Deploy

iTranswarp is deployed by Ansible. Scripts is ready for Ubuntu Server 18.04 x64.

Deploy script:

```
$ ansible/deploy.py --profile <env>
```

The deploy script will do following:

- install open jdk 11 headless;
- install nginx;
- install supervisor;
- deploy jar;
- deploy static resources;
- generate nginx configuration;
- generate supervisor configuration;
- update symbol link;
- reload supervisor;
- reload nginx.
