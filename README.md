#  Construindo uma API Rest de consulta das cidades do Brasil do zero até a produção
 API # Cities

##  Requisitos

* Linux
* Git
* Java 8
* Docker
* Comunidade IntelliJ
* Heroku CLI

##  DataBase

###  Postgres

* [ Postgres Docker Hub ] (https://hub.docker.com/_/postgres)

`` `script de shell
docker run --name cities-db -d -p 5432: 5432 -e POSTGRES_USER = postgres_user_city -e POSTGRES_PASSWORD = super_password -e POSTGRES_DB = cidades postgres
`` `

###  Preencher

* [ dados ] (https://github.com/chinnonsantos/sql-paises-estados-cidades/tree/master/PostgreSQL)

`` `script de shell
cd ~ / workspace / sql-paises-estados-cidades / PostgreSQL
docker run -it --rm --net = host -v $ PWD: / tmp postgres / bin / bash
psql -h localhost -U postgres_user_city cities -f /tmp/pais.sql
psql -h localhost -U postgres_user_city cities -f /tmp/estado.sql
psql -h localhost -U postgres_user_city cities -f /tmp/cidade.sql
psql -h localhost -U postgres_user_city cities
CRIAR cubo de EXTENSÃO; 
CRIAR EXTENSÃO distância da terra;
`` `

* [ Postgres Earth distance ] (https://www.postgresql.org/docs/current/earthdistance.html)
* [ earthdistance - 1.0--1.1.sql ] (https://github.com/postgres/postgres/blob/master/contrib/earthdistance/earthdistance--1.0--1.1.sql)
* [ OPERADOR <@> ] (https://github.com/postgres/postgres/blob/master/contrib/earthdistance/earthdistance--1.1.sql)
* [ postgrescheatsheet ] (https://postgrescheatsheet.com/#/tables)
* [ datatype-geometric ] (https://www.postgresql.org/docs/current/datatype-geometric.html)

###  Acesso

`` `script de shell
docker exec -it cities-db / bin / bash
psql -U postgres_user_city cities
`` `

###  Consulta à distância da Terra

Apontar
`` `roomsql
selecionar (( selecionar  lat_lon  da  cidade  onde  id  =  4929 ) < @ > ( selecionar  lat_lon  da  cidade  onde  id = 5254 )) como  distância ;
`` `

Cubo
`` `roomsql
selecione earth_distance (
    ll_to_earth ( - 21.95840072631836 , - 47.98820114135742 ),
    ll_to_earth ( - 22.01740074157715 , - 47.88600158691406 )
) como  distância ;
`` `

##  Spring Boot

* [ https://start.spring.io/ ] (https://start.spring.io/)

+ Java 8
+ Projeto Gradle
+ Jar
+ Spring Web
+ Spring Data JPA
+ Driver PostgreSQL

###  Spring Data

* [ jpa.query-methods ] (https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods)

###  Propriedades

* [ propriedades do aplicativo apêndice ] (https://docs.spring.io/spring-boot/docs/current/reference/html/apencha-application-properties.html)
* [ jdbc-database-connectio ] (https://www.codejava.net/java-se/jdbc/jdbc-database-connection-url-for-common-databases)

###  Tipos

* [ JsonTypes ] (https://github.com/vladmihalcea/hibernate-types)
* [ UserType ] (https://docs.jboss.org/hibernate/orm/3.5/api/org/hibernate/usertype/UserType.html)

##  Heroku

* [ DevCenter ] (https://devcenter.heroku.com/articles/getting-started-with-gradle-on-heroku)

##  Qualidade do Código

###  PMD

+ https://pmd.github.io/pmd-6.8.0/index.html

###  Checkstyle

+ https://checkstyle.org/

+ https://checkstyle.org/google_style.html

+ http://google.github.io/styleguide/javaguide.html

`` `script de shell
wget https://raw.githubusercontent.com/checkstyle/checkstyle/master/src/main/resources/google_checks.xml
`` `
