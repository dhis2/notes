# Mac OSX

* Fork [dhis2-core](https://github.com/dhis2/dhis2-core) and git clone it to your machine

* Use branch **master**

* Install Postgres (i.e. using homebrew `brew install postgres`)

* Install jdk 8, [get it here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 

* Set your JAVA_HOME to jdk 8 (9 will not work), i.e. add the following line to your ~/.profile:
    ```shell
    export JAVA_HOME=`/System/Library/Frameworks/JavaVM.framework/Versions/Current/commands/java_home`
    ```

* Install apache-tomcat (i.e. using homebrew `brew install tomcat`)

* Install Maven (i.e. using homebrew `brew install maven`)

* Generate DHIS2 War:

    * At source code go to dhis-2 folder and execute `mvn -Dmaven.test.failure.ignore=true clean install`

    * Go to dhis-2/dhis-web and execute `mvn -Dmaven.test.failure.ignore=true clean install`

    * A dhis.war file will be generated at dhis-2/dhis-web/dhis-web-portal/target. Copy this file.

* Go to your to your Tomcat webapps folder and paste the generated dhis.war file 

* [OPTIONAL] Go to your Tomcat conf folder and update the tomcat-users.xml file so that you have a user that has access to the web manager which can start and stop the app. Add the lines below before the end of the XML file:
    ```xml
    <role rolename="manager-gui"/>
    <user username="tomcat" password="tomcat" roles="manager-gui"/>
    ```
* At your Tomcat bin folder create a setenv&#46;sh file where you define DHIS2_HOME environment variable which will be pointing for needed configurations (for example): `export DHIS2_HOME=~/dhis2_home`

* At your DHIS2_HOME you should place 1 file: dhis.conf (an example is shared below)

* Create a Postgres Database with name, role and password and update dhis.conf accordingly (example assumes name, role and password to be **dhis**)

* Import one of the databases shared at [dhis2-demo-db](https://github.com/dhis2/dhis2-demo-db). If this step is skipped a clean DHIS2 instance will installed and will work properly

* Start your tomcat (e.g. `./startup.sh && tail -f ../logs/catalina.out`);

* Go to [http://localhost:8080/dhis](http://localhost:8080/dhis) to visit your local instance of dhis2-core

* [OPTIONAL] When you reboot, tomcat will not start automatically. If you want tomcat to start upon login, and you have installed it via homebrew, you can do `brew services start tomcat`

* [OPTIONAL] If you want to locally work on front-end apps, make sure to add http://localhost:8081 to your CORS whitelist in the dhis-core app via `>apps>system_settings>access>cors_whitelist`

### dhis.conf

    # Hibernate SQL dialect
    connection.dialect = org.hibernate.dialect.PostgreSQLDialect
    # JDBC driver class
    connection.driver_class = org.postgresql.Driver
    # Database connection URL
    connection.url = jdbc:postgresql://localhost/dhis
    # Database username
    connection.username = dhis
    # Database password
    connection.password = dhis
    # Database schema behavior, can be validate, update, create, create-drop
    connection.schema = update

# Linux (Debian 9)

| symbol | meaning |
| --- | --- |
| `#` | run command as root |
| `$` | run command as user |
| `%` | run command inside app |
| ` ` | relevant output from cmd |
| `--` | comment |

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

-- build the `dhis.war` under `dhis-web/dhis-web-portal/target` 
$ cd dhis-web
$ mvn clean install

-- this deploys dhis2 to tomcat 
$ sudo cp /opt/dhis2/dhis2-core/dhis-2/dhis-web/dhis-web-portal/target/dhis.war /var/lib/tomcat8/webapps/

-- monitor the deployment
$ sudo tail -f /var/log/tomcat8/catalina.out

...
25-Jan-2018 10:29:22.161 INFO [localhost-startStop-3] org.apache.catalina.start
up.HostConfig.deployWAR Deploying web application archive /var/lib/tomcat8/weba
pps/dhis.war
...
25-Jan-2018 10:30:45.970 INFO [localhost-startStop-3] org.apache.catalina.start
up.HostConfig.deployWAR Deployment of web application archive /var/lib/tomcat8/
webapps/dhis.war has finished in 83,809 ms

-- test that everything works
$ curl -i -L http://localhost:8080/dhis

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
