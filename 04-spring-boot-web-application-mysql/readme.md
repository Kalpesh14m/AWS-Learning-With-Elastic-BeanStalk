# Todo Web Application using Spring Boot and MySQL as Database

Run com.bunny.springboot.web.SpringBootFirstWebApplication as a Java Application.

Runs on default port of Spring Boot - 8080

Application uses h2 database to run the tests.

## Can be run as a Jar or a WAR

`mvn clean install` generate a war which can deployed to your favorite web server.

We will deploy to Cloud as a WAR

## Web Application

- http://localhost:8080/login with bunny/dummy as credentials
- You can add, delete and update your todos
- Spring Security is used to secure the application
- `com.bunny.springboot.web.security.SecurityConfiguration` contains the in memory security credential configuration.


## Changes from H2 Application

#### pom.xml

```
<dependency>
	<groupId>com.h2database</groupId>
	<artifactId>h2</artifactId>
	<scope>test</scope>
</dependency>

<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
</dependency>
```

#### src/main/resources/application.properties

```
#spring.h2.console.enabled=true
#spring.h2.console.settings.web-allow-others=true

spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://${RDS_HOSTNAME:localhost}:${RDS_PORT:3306}/${RDS_DB_NAME:todos}
spring.datasource.username=${RDS_USERNAME:kalpesh}
spring.datasource.password=${RDS_PASSWORD:dummytodos}
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL57Dialect
```

#### src/test/resources/application.properties

```
spring.jpa.hibernate.ddl-auto=create-drop
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.url=jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1
spring.datasource.username=sa
spring.datasource.password=sa
```

#### public class Todo

```
@Size(min=10, message="Enter at least 10 Characters...")
@Column(name="description")
private String desc;
```
## My SQL

### Launching MySQL using Docker

```
docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=kalpesh --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 mysql:5.7
```


### My SQL Shell Client

- https://dev.mysql.com/downloads/shell/


Server version: 5.7.26 MySQL Community Server (GPL)
No default schema selected; type \use <schema> to set one.

 MySQL  localhost:3306 ssl  JS > \sql
Switching to SQL mode... Commands end with ;

 MySQL  localhost:3306 ssl  SQL > use todos
Default schema set to `todos`.
Fetching table and column names from `todos` for auto-completion... Press ^C to stop.

 MySQL  localhost:3306 ssl  todos  SQL > select * from todo ;
+----+--------------+---------+----------------------------+-------------+
| id | description  | is_done | target_date                | user        |
+----+--------------+---------+----------------------------+-------------+
|  1 | Default Desc | 0       | 2019-06-26 18:30:00.000000 | bunny 	 |
+----+--------------+---------+----------------------------+-------------+
1 row in set (0.0032 sec)

### Create Todo Table for Production

```
create table hibernate_sequence (next_val bigint) engine=InnoDB
insert into hibernate_sequence values ( 1 )
create table todo (id integer not null, description varchar(255), is_done bit not null, target_date datetime(6), user varchar(255), primary key (id)) engine=InnoDB
```

![](https://user-images.githubusercontent.com/25608527/83552507-844a7080-a527-11ea-8d24-bb02a986c36b.png)

![](https://user-images.githubusercontent.com/25608527/83552510-87ddf780-a527-11ea-942b-73404fb206e8.png)

![](https://user-images.githubusercontent.com/25608527/83552513-890f2480-a527-11ea-8b32-2e2b99651f4b.png)

![](https://user-images.githubusercontent.com/25608527/83552521-8b717e80-a527-11ea-912b-8c2cc9a5d3f5.png)

![](https://user-images.githubusercontent.com/25608527/83552526-8ca2ab80-a527-11ea-9b6a-cef0e14a2f9d.png)

![](https://user-images.githubusercontent.com/25608527/83552534-8e6c6f00-a527-11ea-94ae-4ee9bba39448.png)

![](https://user-images.githubusercontent.com/25608527/83552539-8f9d9c00-a527-11ea-8dad-3c2403452ec5.png)

![](https://user-images.githubusercontent.com/25608527/83552542-90cec900-a527-11ea-8642-3dab23b85434.png)

![](https://user-images.githubusercontent.com/25608527/83552551-93c9b980-a527-11ea-8d84-9656e7709521.png)

![](https://user-images.githubusercontent.com/25608527/83552554-95937d00-a527-11ea-94eb-aa4577589558.png)

![](https://user-images.githubusercontent.com/25608527/83552563-97f5d700-a527-11ea-8057-239e4490d77d.png)

## full version of command

![](https://user-images.githubusercontent.com/25608527/83552568-99bf9a80-a527-11ea-9277-50029662b8a1.png)

![](https://user-images.githubusercontent.com/25608527/83552575-9c21f480-a527-11ea-8fa0-21116ba06bfd.png)

![](https://user-images.githubusercontent.com/25608527/83552579-9d532180-a527-11ea-838f-3bd1d4fbcdc8.png)

![](https://user-images.githubusercontent.com/25608527/83552587-a04e1200-a527-11ea-8e61-89ef17bdeccb.png)

![](https://user-images.githubusercontent.com/25608527/83552591-a2b06c00-a527-11ea-8c43-c9695c479697.png)

![](https://user-images.githubusercontent.com/25608527/83552593-a3e19900-a527-11ea-9fef-bd832ed1b5b2.png)

![](https://user-images.githubusercontent.com/25608527/83552598-a512c600-a527-11ea-92e9-a7c286f1b350.png)

![](https://user-images.githubusercontent.com/25608527/83552616-ab08a700-a527-11ea-816b-3e7d01dbdd43.png)

![](https://user-images.githubusercontent.com/25608527/83552620-acd26a80-a527-11ea-8515-179173193627.png)

![](https://user-images.githubusercontent.com/25608527/83552804-fa4ed780-a527-11ea-84f4-548fe339e0d0.png)

![](https://user-images.githubusercontent.com/25608527/83552825-0044b880-a528-11ea-9324-84f72a3994bf.png)

![](https://user-images.githubusercontent.com/25608527/83552830-0175e580-a528-11ea-847b-a8f547d91779.png)

![](https://user-images.githubusercontent.com/25608527/83552840-033fa900-a528-11ea-872a-cec7ae7b4161.png)

![](https://user-images.githubusercontent.com/25608527/83552878-12bef200-a528-11ea-9d33-0aa409c72887.png)

![](https://user-images.githubusercontent.com/25608527/83552881-13f01f00-a528-11ea-8da8-cb2ec271bc54.png)

![](https://user-images.githubusercontent.com/25608527/83552883-15b9e280-a528-11ea-8257-6f6b5ac82967.png)

![](https://user-images.githubusercontent.com/25608527/83552888-16eb0f80-a528-11ea-86be-102fc88dc067.png)

![](https://user-images.githubusercontent.com/25608527/83552895-194d6980-a528-11ea-8194-630760b6ef41.png)

![](https://user-images.githubusercontent.com/25608527/83552900-1a7e9680-a528-11ea-83d6-0229d355b31c.png)

![](https://user-images.githubusercontent.com/25608527/83552913-1fdbe100-a528-11ea-8740-f5408e9db2a7.png)

![](https://user-images.githubusercontent.com/25608527/83552923-21a5a480-a528-11ea-9cb2-19d0454c65eb.png)

![](https://user-images.githubusercontent.com/25608527/83552937-2407fe80-a528-11ea-93cc-117f154ff3b8.png)

![](https://user-images.githubusercontent.com/25608527/83552945-25d1c200-a528-11ea-9dcf-da65a58a38bc.png)

![](https://user-images.githubusercontent.com/25608527/83552950-279b8580-a528-11ea-9a75-6d02114de7af.png)

![](https://user-images.githubusercontent.com/25608527/83552962-29fddf80-a528-11ea-95dc-539f30b7c989.png)

![](https://user-images.githubusercontent.com/25608527/83552965-2c603980-a528-11ea-9608-ef9497787e11.png)

![](https://user-images.githubusercontent.com/25608527/83552972-2e29fd00-a528-11ea-8fae-6349fe36c208.png)

![](https://user-images.githubusercontent.com/25608527/83553121-6af5f400-a528-11ea-863e-62062947eb2c.png)

![](https://user-images.githubusercontent.com/25608527/83553132-6cbfb780-a528-11ea-8d14-7c3a5ff76db4.png)

![](https://user-images.githubusercontent.com/25608527/83553144-6f221180-a528-11ea-8a5d-bfec601133cd.png)

![](https://user-images.githubusercontent.com/25608527/83553147-70533e80-a528-11ea-8967-a0150deb4b06.png)

![](https://user-images.githubusercontent.com/25608527/83553157-72b59880-a528-11ea-84bd-6f391d3ce703.png)

![](https://user-images.githubusercontent.com/25608527/83553162-747f5c00-a528-11ea-86ea-00183aaff3b2.png)

![](https://user-images.githubusercontent.com/25608527/83553170-76491f80-a528-11ea-8b8c-c237bf9b06d3.png)

![](https://user-images.githubusercontent.com/25608527/83553180-7812e300-a528-11ea-80e9-7ab80bbeddc8.png)

![](https://user-images.githubusercontent.com/25608527/83553188-79dca680-a528-11ea-9dda-8a83eb12297c.png)

![](https://user-images.githubusercontent.com/25608527/83553193-7ba66a00-a528-11ea-9214-239ce51bb069.png)

![](https://user-images.githubusercontent.com/25608527/83553204-7ea15a80-a528-11ea-84c7-59fd4a63645a.png)

![](https://user-images.githubusercontent.com/25608527/83553207-7fd28780-a528-11ea-8cd2-344be5ad643f.png)

![](https://user-images.githubusercontent.com/25608527/83553209-819c4b00-a528-11ea-9f3a-c66bf402dd7d.png)

![](https://user-images.githubusercontent.com/25608527/83553211-82cd7800-a528-11ea-8179-2d96868e433c.png)

## Security Group will allow TCP traffic on port 80

![](https://user-images.githubusercontent.com/25608527/83553215-84973b80-a528-11ea-9795-5d38824e1830.png)

![](https://user-images.githubusercontent.com/25608527/83553221-86f99580-a528-11ea-9779-c510a7d09bcb.png)

![](https://user-images.githubusercontent.com/25608527/83553226-882ac280-a528-11ea-90c9-9caea81e8e12.png)

![](https://user-images.githubusercontent.com/25608527/83553230-89f48600-a528-11ea-8f6e-1d90d1fb4df9.png)

![](https://user-images.githubusercontent.com/25608527/83553235-8bbe4980-a528-11ea-93b1-164b6f54a528.png)

![](https://user-images.githubusercontent.com/25608527/83553242-8d880d00-a528-11ea-91fb-dfef93e516fb.png)

![](https://user-images.githubusercontent.com/25608527/83553246-8eb93a00-a528-11ea-803f-f4352f38988e.png)

![](https://user-images.githubusercontent.com/25608527/83553249-9082fd80-a528-11ea-826c-530e8cefb286.png)

![](https://user-images.githubusercontent.com/25608527/83553253-92e55780-a528-11ea-97ec-d7980bbdab8f.png)

![](https://user-images.githubusercontent.com/25608527/83553259-94168480-a528-11ea-820b-f5fa145c55d8.png)

![](https://user-images.githubusercontent.com/25608527/83553262-9547b180-a528-11ea-8475-0733c4f5db64.png)

![](https://user-images.githubusercontent.com/25608527/83553264-97aa0b80-a528-11ea-8ba5-81805ae43812.png)

![](https://user-images.githubusercontent.com/25608527/83553272-98db3880-a528-11ea-952b-80725158de5d.png)

![](https://user-images.githubusercontent.com/25608527/83553277-9aa4fc00-a528-11ea-9743-558a96979534.png)

![](https://user-images.githubusercontent.com/25608527/83553290-9d075600-a528-11ea-9aa0-f45f1dac9a7d.png)

![](https://user-images.githubusercontent.com/25608527/83553297-9e388300-a528-11ea-965c-05bcaf795363.png)

![](https://user-images.githubusercontent.com/25608527/83553303-9f69b000-a528-11ea-9160-8faad0d4d43c.png)

![](https://user-images.githubusercontent.com/25608527/83553310-a1337380-a528-11ea-9e4c-3ef7891c2e09.png)

![](https://user-images.githubusercontent.com/25608527/83553313-a264a080-a528-11ea-94c0-f63c66fa3484.png)

![](https://user-images.githubusercontent.com/25608527/83554551-9ed21900-a52a-11ea-8b85-8d8fbc1136ed.png)

![](https://user-images.githubusercontent.com/25608527/83553322-a5f82780-a528-11ea-8ba5-e55fa245b2cd.png)

![](https://user-images.githubusercontent.com/25608527/83553317-a42e6400-a528-11ea-9381-0a1567c6460f.png)

![](https://user-images.githubusercontent.com/25608527/83553329-a98bae80-a528-11ea-9d92-d9de08c66911.png)

