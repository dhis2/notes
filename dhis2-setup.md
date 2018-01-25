# Linux (Debian 9)

| symbol | meaning |
| --- | --- |
| `#` | run command as root |
| `$` | run command as user |
| `%` | run command inside app |
| ` ` | relevant output from cmd |

## Prepare the distro

```
# adduser dhis
# mkdir /opt/dhis2
# apt install maven curl vim openjdk-8 openjdk-8-jre git
```

Either `chmod` loose permissions to `/opt/dhis2` or `chown` it to the
user you want.

## Setup Tomcat
```
$ sudo apt install tomcat8
$ sudo systemctl enable tomcat8
$ sudo systemctl start tomcat8
```

## Setup the Database

```
$ sudo apt install postgresql-9.6
$ sudo systemctl enable postgresql@9.6-main.service
$ sudo systemctl start postgresql@9.6-main.service
$ sudo -u postgres psql
% create user 'dhis' with password 'dhis';
% create database "dhis2";
% grant all privileges on database "dhis2" to dhis;
% \q
```

### Load demo data into database

```
$ curl -o dhis2-demo.zip https://www.dhis2.org/download/resources/2.28/dhis2-demo.zip
$ unzip dhis2-demo.zip
$ sudo -u postgres psql -d dhis2 -U dhis -f demo.sql
```

### Update 2.28 database to 2.29
```
$ curl -o upgrade-229.sql https://raw.githubusercontent.com/dhis2/dhis2-utils/master/resources/sql/upgrade-229.sql
$ sudo -u postgres psql -d dhis2 -U dhis -f upgrade-229.sql
```

## Setup the DHIS2 software

```
$ git clone git@github.com:dhis2/dhis2-core.git /opt/dhis2/dhis2-core
$ vim /opt/dhis2/dhis.conf
% connection.dialect = org.hibernate.dialect.PostgreSQLDialect
% connection.driver_class = org.postgresql.Driver
% connection.url = jdbc:postgresql:dhis2
% connection.username = dhis
% connection.password = dhis
% connection.schema = update
% encryption.password = xxxx

$ cd /opt/dhis2/dhis2-core/dhis-2
$ mvn clean install
$ cd dhis-web
$ mvn clean install # builds the `dhis.war` under `dhis-web/dhis-web-portal/target`
$ sudo cp /opt/dhis2/dhis2-core/dhis-2/dhis-web/dhis-web-portal/target/dhis.war /var/lib/tomcat8/webapps/ # this deploys dhis2 to tomcat

$ sudo tail -f /var/log/tomcat8/catalina.out # monitor the deployment
...
25-Jan-2018 10:29:22.161 INFO [localhost-startStop-3] org.apache.catalina.start
up.HostConfig.deployWAR Deploying web application archive /var/lib/tomcat8/weba
pps/dhis.war
...
25-Jan-2018 10:30:45.970 INFO [localhost-startStop-3] org.apache.catalina.start
up.HostConfig.deployWAR Deployment of web application archive /var/lib/tomcat8/
webapps/dhis.war has finished in 83,809 ms

$ curl -i -L http://localhost:8080/dhis # test that it works

HTTP/1.1 302
Location: /dhis/
Transfer-Encoding: chunked
Date: Thu, 25 Jan 2018 10:36:12 GMT

HTTP/1.1 302
Location: dhis-web-commons-about/redirect.action
Content-Length: 0
Date: Thu, 25 Jan 2018 10:36:12 GMT

HTTP/1.1 302
X-XSS-Protection: 1; mode=block
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Set-Cookie: JSESSIONID=2D389C3BA604089B545B95CFB9DFC8F0; Path=/dhis; HttpOnly
Location: http://localhost:8080/dhis/dhis-web-commons/security/login.action
Content-Length: 0
Date: Thu, 25 Jan 2018 10:36:12 GMT

HTTP/1.1 200
X-XSS-Protection: 1; mode=block
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Set-Cookie: JSESSIONID=A0F13BCD6E81A5FDD5C66EAFEBE8DCE4; Path=/dhis; HttpOnly
Cache-Control: no-cache, no-store, max-age=0, must-revalidate
Login-Page: true
Content-Type: text/html;charset=UTF-8
Transfer-Encoding: chunked
Date: Thu, 25 Jan 2018 10:36:12 GMT

<!DOCTYPE HTML>
...
```

At this point your Tomcat is serving DHIS2 on http://localhost:8080/dhis
and you can use this URL for your frontend apps.
