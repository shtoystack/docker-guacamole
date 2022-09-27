**This is a fork of oznu/docker-guacamole, updated to tomcat9.0.65 (guacamole is not compatible with tomcat10), postgresql 14, guacamole 1.4.0, and s6_overlay 3.1.**


**If you are looking to upgrade from Oznu's image, or from an image that uses a version of PostgreSQL lower than 13, please have a look at the  [upgrade instructions](https://github.com/abesnier/docker-guacamole/blob/master/UPGRADE.md). It is written for my images, but can be adapted for any image.**

**Every month, inactive images on Docker Hub will be removed. If you use one of those, you'll need to update to a newer image.**


# Summary of images
Base OS | PostgreSQL 13 | PostgreSQL 14
---|---|---
Bullseye | guacamole:1.4.0-bullseye | N/A
Ubuntu | guacamole:1.4.0 | guacamole:1.4.0-pg14


# What's new / Changelog
**2022-09-27** - All tags updated to Tomcat 9.0.67.

**2022-08-30** - All tags updated to S6 Overlay v3.1.2.1.

**2022-08-29** - All tags updated to S6 Overlay v3.1.2.0.

**2022-08-24** - All tags updated to PostgreSQL JDBC 42.5.0 (yes, the same day I updated them to 42.4.2, the wonderful PostgreSQL JDBC team released another version...)

**2022-08-24** - All tags updated to PostgreSQL JDBC 42.4.2

**2022-08-09** - Added an extension `guacamole-branding-1.4.0.jar`. It now comes enabled by default, and its sole effect is to add links to the official Apache Guacamole webpage, to my github, and to the issue page on github.

The idea of this extension is to show that even a docker image can use the branding possibilities of Guacamole. If you have an existing branding extension, you can just drop it in the `config/guacamole/extensions` directory and restart the container.

**2022-08-05** - All tags reverted to PostgresJDBC 42.4.0, as it appears images cannot start properly with 42.4.1. I need to investigate why, but I noticed an fatal error during some random testing: 

`### Error querying database. Cause: java.sql.SQLException: Error setting driver on UnpooledDataSource. Cause: java.lang.ClassNotFoundException: org.postgresql.Driver`

So I decided to rebuild the image with 42.4.0. I will continue testing until resolved.


**2022-08-04** - All tags updated to PostgresJDBC 42.4.1

**2022-07-22** - All tags updated to Tomcat 9.0.65

**2022-07-01** - Follow up on moving from the base image to Ubuntu Jammy (22.04.4 LTS). The default postgresql package is in version [14.3](https://packages.ubuntu.com/jammy/postgresql), and if you inspect the Dockerfiles, you will see that I need to add the official postgres repository to be able to install postgresql-13.


I don't like that, as I am used to using Debian, and learnt not to mix repositories if you can avoid it.


So, I have created a new tag "latest-pg14" in order to test the upgrade process. And it is surprisingly easy. Please have a look at the [upgrade instructions](https://github.com/abesnier/docker-guacamole/blob/master/UPGRADE.md) for details, should you chose to upgrade.


**2022-06-30** - Well ,well, well, the base Tomcat image never ceases to amaze me! Since the last image re-build the base image has now moved to Ubuntu Jammy (22.04.4 LTS). This came with an unexpected surprise: OpenSSL has been upgraded to 3.0.2. This might seem innocuous, but the build process of Guacamole Server failed, as it relies on deprecated methods. Source code for Guacamole has already been updated on GitHub, but not the downloadable source tarball from the official website.


So, the latest tag is now built on the source code available on Github.


Oh, and by the way, updated to s6 overlay 3.1.1.2.


**2022-06-27** - New tags are available!  The philosophy for tomcat base image (i.e. 9.0.64-jre11) is to switch from openjdk to Temurin, but unfortunately, the build process failed with this base image. 9.0.64-jre11 used to be based on Debian Bullseye, but it is now based on Ubuntu 20.04.4 LTS. So I decided to create new tags:


* 1.4.0, latest : based on tomcat:9.0.64-jre11, which is based on Ubuntu 20.04.4 LTS

* 1.4.0-bullseye, latest-bullseye : based on tomcat:9.0.64-jre11-openjdb-slim-bullseye

* the *-bullseye images will work as before, and I have tested the Ubuntu-based ones as much as I could. Please report  [issues](https://github.com/abesnier/docker-guacamole/issues) if any, I'll make my best to solve them as fast as possible! 


Oh, and by the way, updated to s6 overlay 3.1.1.1


**2022-06-10** - updated to tomcat 9.0.64 and PostGresJDBC 42.4.0


**2022-05-11** - updated to PostgresJDBC 42.3.6


**2022-05-12** - updated to tomcat 9.0.63


**2022-05-12** - added a new tag: github. This image is built on the github repos for guacamole-server and guacamole-client.


**2022-05-11** - updated to PostgresJDBC 42.3.5


**2022-04-19** - updated to Tomcat 9.0.62 and PostgresJDBC 42.3.4


**2022-03-16** - updated to tomcat 9.0.60, and fixed an issue that prevented the container to start on arm64


**2022-03-08** - updated to S6 Overlay 3.1.0.1


**2022-03-01** - updated to PostgresJDBC 42.3.3, tomcat 9.0.59, arm64 not supported by tomcat 9.0.59


**2022-02-22** - updated to s6 overlay 3.0.0.2-2


**2022-02-07** - updated to version Postegres JDBC driver 42.3.2


**2022-01-31** - s6 overlay 3.0.0.2 has been released, that corrects a bug in the management of environment variables. Images 1.4.0, 1.4.0-s6_v3 and latest have been updated to this version, as well as updated to Tomcat 9.0.58.


**2022-01-29** - I noticed a typo in the Dockerfile that introduced a bug with Postgres JDBC Driver. Fixed in all tags. Issue #2


**2022-01-27** - updated to s6 overlay 3.0 and tomcat 9.0.58


**2022-01-03** - updated to version 1.4.0


# Available tags


`1.4.0` `latest` , version 1.4.0, based on latest Tomcat, PostgresJDBC driver and S6 Overlay available at time of build.


`1.3.0` , version 1.3.0, based on latest Tomcat, PostgresJDBC driver available at time of build, and S6 Overlay 2.2.0.3.


`github` compiled from available source code on github for guacamole-client and guacamole-server.


`1.4.0-s6_v3` updated to s6 overlay 3.0.0.0 and tomcat:9.0.58-jre11 (note: This image is built on a custom build of s6 overlay. It will be renamed as latest when s6 overlay is fixed and I can use the [release tarballs](https://github.com/just-containers/s6-overlay/releases/).)


# Auto promo


If Guacamole is useful to you, do not hesitate to support the great work of the [Apache Foundation](https://donate.apache.org/).


On a side note, running the server I use to build these images, researching update info, maintaining the images, takes quite some time and a little money. I'll gladly accept [a coffee!](https://paypal.me/antoinebesnier)


# Docker Guacamole


A Docker Container for [Apache Guacamole](https://guacamole.apache.org/), a client-less remote desktop gateway. It supports standard protocols like VNC, RDP, and SSH over HTML5.


[![IMAGE ALT TEXT](http://img.youtube.com/vi/esgaHNRxdhY/0.jpg)](http://www.youtube.com/watch?v=esgaHNRxdhY "Video Title")


This container runs the guacamole web client, the guacd server and a postgres database.


## Usage


```shell

docker run \

  -p 8080:8080 \

  -v </path/to/config>:/config \

  abesnier/guacamole

```


## Parameters


The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side.


* `-p 8080:8080` - Binds the service to port 8080 on the Docker host, **required**

* `-v /config` - The config and database location, **required**

* `-e EXTENSIONS` - See below for details.


## Enabling Extensions


Extensions can be enabled using the `-e EXTENSIONS` variable. Multiple extensions can be enabled using a comma separated list without spaces.


For example:


```shell

docker run \

  -p 8080:8080 \

  -v </path/to/config>:/config \

  -e "EXTENSIONS=auth-ldap,auth-duo"

  abesnier/guacamole

```


Currently the available extensions are:


* [1.3.0] [1.4.0] auth-ldap - [LDAP Authentication](https://guacamole.apache.org/doc/gug/ldap-auth.html)

* [1.3.0] [1.4.0] auth-duo - [Duo two-factor authentication](https://guacamole.apache.org/doc/gug/duo-auth.html)

* [1.3.0] [1.4.0] auth-header - [HTTP header authentication](https://guacamole.apache.org/doc/gug/header-auth.html)

* [1.3.0] [1.4.0] auth-cas - [CAS Authentication](https://guacamole.apache.org/doc/gug/cas-auth.html)

* [1.3.0] [1.4.0] auth-openid - [OpenID Connect authentication](https://guacamole.apache.org/doc/gug/openid-auth.html)

* [1.3.0] [1.4.0] auth-totp - [TOTP two-factor authentication](https://guacamole.apache.org/doc/gug/totp-auth.html)

* [1.3.0] [1.4.0] auth-quickconnect - [Ad-hoc connections extension](https://guacamole.apache.org/doc/gug/adhoc-connections.html)

* [1.3.0] [1.4.0] auth-saml - [SAML Authentication](https://guacamole.apache.org/doc/gug/saml-auth.html)

* [1.4.0] auth-sso - SSO Authentication metapackage, contains classes for CAS, OpenID and SAML authentication (see links above)

* [1.4.0] auth-json - [Encrypted JSON Authentication](https://guacamole.apache.org/doc/gug/json-auth.html)





You should only enable the extensions you require, if an extensions is not configured correctly in the `guacamole.properties` file it may prevent the system from loading. See the [official documentation](https://guacamole.apache.org/doc/gug/) for more details.


## Default User


The default username is `guacadmin` with password `guacadmin`.


## Windows-based Docker Hosts


Mapped volumes behave differently when running Docker for Windows and you may encounter some issues with PostgreSQL file system permissions. To avoid these issues, and still retain your config between container upgrades and recreation, you can use the local volume driver, as shown in the `docker-compose.yml` example below. When using this setup be careful to gracefully stop the container or data may be lost.


```yml

version: "3"

services:

  guacamole:

    image: abesnier/guacamole

    container_name: guacamole

    volumes:

      - postgres:/config

    ports:

      - 8080:8080

volumes:

  postgres:

    driver: local

```


## Something's not working, what to do?



### Underscore character is not displayed in SSH sessions


There is a know bug, where, in certain conditions, the underscore character is not displayed properly. This issue appeared since Guacamole 1.3, and still exists in 1.4.

Based on some investigations, it seems the issue is with the libpango library (text rendering library), that is used by Guacamole. The issue has been known for quite a few years now by the library team, but unfortunately, it does not look like a solution will ever be found, as it really appears to be quite random and difficult to reproduce.


[![IMAGE ALT TEXT](https://github.com/abesnier/docker-guacamole/raw/master/underscore.png)](https://github.com/abesnier/docker-guacamole/raw/master/underscore.png|width=200px)


Please have a look at this [JIRA issue](https://issues.apache.org/jira/browse/GUACAMOLE-1478?jql=project%20%3D%20GUACAMOLE%20AND%20text%20~%20underscore) for details.


Now, that being said, here's what happens: by default, a new ssh connection will use the default remote machine font (most likely the default monospace font, and in most Linux distros these days, it is DejaVu or Nimbus), with a size 12.

This exact configuration, in some cases will result in the underscore not being displayed.


There are two solutions that worked for me: 

* Change the base image for my Docker image (downgrading from Debian Bullseye to Debian Buster)

* Change the font size in the connection settings


The first solution is not good for me, as the idea of this image is to be kept up-to-date with the latest available packages.


The second solution is easy to implement, but it must be done by the admin. Go to Guacamole > Settings > Connections > Parameters > change the font size to 14 for example > save your changes.


### The container fails to start properly

If the docker seems to not start properly, check the logs  with `docker logs <container_name>`.


If you see lines like this one: `postgres: could not access the server configuration file "/config/postgres/postgresql.conf": No such file or directory`, this means that the configuration volume could not be mounted properly. 


If that is the case, make sure to start the container as root. This will force the creation of the config folder.

```shell

docker run \

  -p 8080:8080 \

  -u root \

  -v </path/to/config>:/config \

  abesnier/guacamole

```


or in docker-compose.yml:


```yml

version: "3"

services:

  guacamole:

    image: abesnier/guacamole

    container_name: guacamole

    user: root

    volumes:

      - </path/to/config>:/config

    ports:

      - 8080:8080

```


### Back up the config folder and start again

Well, I must admit, I managed to break a few things here and there nevertheless...

The easiest way to correct issues is to stop the container, delete the config folder, and restart the container.


But this has the side effect of deleting your stored users and connections as well.


You can backup and restore the database with the following command (assuming your container is named `guacamole`):


Backup: `docker exec -it guacamole bash -c "pg_dump -U guacamole -F t guacamole_db > guacamole_db_backup.tar"`


This creates a `guacamole_db_backup.tar` in your `config` directory that you need to save somewhere else.


Now stop the container, delete the config folder, and restart the container.


To restore the database, copy the backup file in your mounted config folder, and run `docker exec -it guacamole bash -c "pg_restore -d guacamole_db guacamole_db_backup.tar -c -U guacamole"`. You can now login to Guacamole with your user data and should find your connections as you left them.


### Report an issue with the image

Have a look at the [Github repo](https://github.com/abesnier/docker-guacamole), and the [Issues](https://github.com/abesnier/docker-guacamole/issues)page.


### Official support pages

If you believe the issue is with Guacamole and not the docker image, have a lok at the [mailing list](https://lists.apache.org/list.html?user@guacamole.apache.org) for general support, and if you believe there is a bug, use the [bug tracker](https://issues.apache.org/jira/projects/GUACAMOLE/summary) to report it.


And of course, don't forget to look at the [official documentation](https://guacamole.apache.org/doc/gug).



## License


Copyright (C) 2017-2020 oznu


Copyright (C) 2021-2022 abesnier


Apache Guacamole is released under the Apache License version 2.0.


Extensions uses thrid-party modules. To consult the licensing for each module, download the extension from https://guacamole.apache.org/releases/1.4.0/, extract it, and check the content of the `bundled` directory.


This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.


This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the [GNU General Public License](./LICENSE) for more details.
