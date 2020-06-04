

## Running the Application

- REST API - Import `restful-web-services` into Eclipse as Maven Project. Run `com.bunny.rest.webservices.restfulwebservices.RestfulWebServicesApplication` as a Java Application. Check Authentication and REST API Sections for executing REST APIs.
- React Application - Import `frontend/todo-app` into Visual Studio Code. Run `npm install` followed by `npm start`
- http://localhost:4200/ with credentials bunny/dummy

> Look at  `Creating New Users` section for creating new users.

## Deploying Front End to AWS

### Change /frontend/todo-app/src/Constants.js

```
/* For Best Practices https://facebook.github.io/create-react-app/docs/adding-custom-environment-variables*/
//export const API_URL = 'http://localhost:5000'
export const API_URL = 'http://restfulwebservices-env.uhpev7xzpb.us-east-1.elasticbeanstalk.com'
```

### Create Production Build

`npm run build`


### S3 Access for Static Content

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AddPerm",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::fullstack-frontend/*"
        }
    ]
}
```

## Authentication

All REST API are protected by JWT Authentication with Spring Security. 

POST to http://localhost:5000/authenticate

```
{
  "username":"bunny",
  "password":"dummy"
}
```

Response
```
{
"token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJpbjI4bWludXRlcyIsImV4cCI6MTU2MjIzNDM1OSwiaWF0IjoxNTYxNjI5NTU5fQ.yvkFtYAp8yGClDo7D5wtXyPSnUPtxu8A7A9YCl9FJdjR0di_yAaPcSTR6liN5bIu1SnOJuSZp94pYSYzU_BNEw"
}
```

Use the token in the headers for all subsequent requests.

`Authorization` : `Bearer ${token}`

Example 

`Authorization` : `Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJpbjI4bWludXRlcyIsImV4cCI6MTU2MjIzNDM1OSwiaWF0IjoxNTYxNjI5NTU5fQ.yvkFtYAp8yGClDo7D5wtXyPSnUPtxu8A7A9YCl9FJdjR0di_yAaPcSTR6liN5bIu1SnOJuSZp94pYSYzU_BNEw`


## Creating New Users

Look at /src/main/resources/data.sql for existing users.

You can create new users by encrypting password with Bcrypt - Use Rounds 10 - https://www.browserling.com/tools/bcrypt 

```
INSERT INTO USER (ID, USERNAME, PASSWORD, ROLE) 
VALUES (3, 'USERNAME', 'BCRYPT_ENCRyPTED_PASSWORD','ROLE_USER');
```


## Hello World URLS

- http://localhost:5000/hello-world

```txt
Hello World
```

- http://localhost:5000/hello-world-bean

```json
{"message":"Hello World - Changed"}
```

- http://localhost:5000/hello-world/path-variable/bunny

```json
{"message":"Hello World, bunny"}
```

## TODO Resource Details

- GET - http://localhost:5000/jpa/users/bunny/todos

```
[
  {
    "id": 10001,
    "username": "bunny",
    "description": "Learn JPA",
    "targetDate": "2019-06-27T06:30:30.696+0000",
    "done": false
  },
  {
    "id": 10002,
    "username": "bunny",
    "description": "Learn Data JPA",
    "targetDate": "2019-06-27T06:30:30.700+0000",
    "done": false
  },
  {
    "id": 10003,
    "username": "bunny",
    "description": "Learn Microservices",
    "targetDate": "2019-06-27T06:30:30.701+0000",
    "done": false
  }
]
```

#### Retrieve a specific todo

- GET - http://localhost:5000/jpa/users/bunny/todos/10001

```
{
  "id": 10001,
  "username": "bunny",
  "description": "Learn JPA",
  "targetDate": "2019-06-27T06:30:30.696+0000",
  "done": false
}
```

#### Creating a new todo

- POST to http://localhost:5000/jpa/users/bunny/todos with BODY of Request given below

```
{
  "username": "bunny",
  "description": "Learn to Drive a Car",
  "targetDate": "2030-11-09T10:49:23.566+0000",
  "done": false
}
```

#### Updating a new todo

- http://localhost:5000/jpa/users/bunny/todos/10001 with BODY of Request given below

```
{
  "id": 10001,
  "username": "bunny",
  "description": "Learn to Drive a Car",
  "targetDate": "2045-11-09T10:49:23.566+0000",
  "done": false
}
```

#### Delete todo

- DELETE to http://localhost:5000/jpa/users/bunny/todos/10001

## H2 Schema - Created by Spring Boot Auto Configuration

```
Hibernate: drop table todo if exists
Hibernate: drop table user if exists
Hibernate: drop sequence if exists hibernate_sequence
Hibernate: drop sequence if exists user_seq
Hibernate: create sequence hibernate_sequence start with 1 increment by 1
Hibernate: create sequence user_seq start with 1 increment by 1
Hibernate: create table todo (id bigint not null, description varchar(255), is_done boolean not null, target_date timestamp, username varchar(255), primary key (id))
Hibernate: create table user (id bigint not null, password varchar(100) not null, role varchar(100) not null, username varchar(50) not null, primary key (id))
Hibernate: alter table user add constraint UK_sb8bbouer5wak8vyiiy4pf2bx unique (username)
```


## H2 Console

- http://localhost:5000/h2-console
- Use `jdbc:h2:mem:testdb` as JDBC URL 



![1](https://user-images.githubusercontent.com/25608527/83811859-30cb5480-a6d8-11ea-8af1-e966c3599126.png)
![2](https://user-images.githubusercontent.com/25608527/83811861-31fc8180-a6d8-11ea-8aa5-fb4f773701f4.png)
![3](https://user-images.githubusercontent.com/25608527/83811867-332dae80-a6d8-11ea-8eb0-d2c2fe5a92f2.png)
![4](https://user-images.githubusercontent.com/25608527/83811869-345edb80-a6d8-11ea-8c31-3036bcbf0385.png)
![5](https://user-images.githubusercontent.com/25608527/83811871-35900880-a6d8-11ea-832e-46c79de9cab9.png)
![6](https://user-images.githubusercontent.com/25608527/83811874-36c13580-a6d8-11ea-95be-30a94914dc05.png)
![7](https://user-images.githubusercontent.com/25608527/83811878-37f26280-a6d8-11ea-9487-0dac3a6d133c.png)
![8](https://user-images.githubusercontent.com/25608527/83811882-39238f80-a6d8-11ea-8035-731fe930fe25.png)
![9](https://user-images.githubusercontent.com/25608527/83811884-3a54bc80-a6d8-11ea-88e3-6e83251b6c22.png)
![10](https://user-images.githubusercontent.com/25608527/83811886-3b85e980-a6d8-11ea-8942-e46cdd5e0bd0.png)
![11](https://user-images.githubusercontent.com/25608527/83811890-3d4fad00-a6d8-11ea-9aa4-fee9db028241.png)
![12](https://user-images.githubusercontent.com/25608527/83811893-3e80da00-a6d8-11ea-9bf1-3e90c55999eb.png)
![13](https://user-images.githubusercontent.com/25608527/83811915-46407e80-a6d8-11ea-9655-17b81b2064da.png)
![14](https://user-images.githubusercontent.com/25608527/83811923-4a6c9c00-a6d8-11ea-995b-62b2c25c24ff.png)
![15](https://user-images.githubusercontent.com/25608527/83811925-4b9dc900-a6d8-11ea-8dc9-3417b316b922.png)
![16](https://user-images.githubusercontent.com/25608527/83811930-4d678c80-a6d8-11ea-898c-065190ba7097.png)
![17](https://user-images.githubusercontent.com/25608527/83811932-4e98b980-a6d8-11ea-9d27-1f848445b116.png)
![18](https://user-images.githubusercontent.com/25608527/83811934-4fc9e680-a6d8-11ea-9fc0-97a3da27e4f7.png)
![19](https://user-images.githubusercontent.com/25608527/83811937-50fb1380-a6d8-11ea-942a-000146d57765.png)
![20](https://user-images.githubusercontent.com/25608527/83811946-522c4080-a6d8-11ea-8f91-77ad98e1a182.png)
![21](https://user-images.githubusercontent.com/25608527/83811949-535d6d80-a6d8-11ea-9d91-838f8e5432d1.png)
![22](https://user-images.githubusercontent.com/25608527/83811953-548e9a80-a6d8-11ea-88c8-4fde0e2f76db.png)
![23](https://user-images.githubusercontent.com/25608527/83811956-55bfc780-a6d8-11ea-8896-ce129f3592e4.png)
![24](https://user-images.githubusercontent.com/25608527/83811958-56f0f480-a6d8-11ea-8756-7ad944652a5c.png)
![25](https://user-images.githubusercontent.com/25608527/83811960-58222180-a6d8-11ea-8197-b7c07a3f183c.png)
![26](https://user-images.githubusercontent.com/25608527/83811963-59534e80-a6d8-11ea-8406-0e96be09ae12.png)
![27](https://user-images.githubusercontent.com/25608527/83811966-5b1d1200-a6d8-11ea-9036-92ad926adf41.png)
![28](https://user-images.githubusercontent.com/25608527/83811970-5c4e3f00-a6d8-11ea-96d7-c820165fd8ea.png)
![29](https://user-images.githubusercontent.com/25608527/83811974-5d7f6c00-a6d8-11ea-97df-eca654139ba3.png)
![30](https://user-images.githubusercontent.com/25608527/83811978-5eb09900-a6d8-11ea-86f3-1b44e58b26c4.png)
![31](https://user-images.githubusercontent.com/25608527/83811981-5fe1c600-a6d8-11ea-83e1-29c26c00e869.png)
![32](https://user-images.githubusercontent.com/25608527/83811986-6112f300-a6d8-11ea-970c-2e43e6b746ff.png)
![33](https://user-images.githubusercontent.com/25608527/83811989-640de380-a6d8-11ea-91ee-9f4a646ef81c.png)
![34](https://user-images.githubusercontent.com/25608527/83811993-653f1080-a6d8-11ea-9add-c3d2e669098b.png)
![35](https://user-images.githubusercontent.com/25608527/83811999-66703d80-a6d8-11ea-893a-b2f352b24983.png)
![36](https://user-images.githubusercontent.com/25608527/83812002-683a0100-a6d8-11ea-965e-a2e225579183.png)
![37](https://user-images.githubusercontent.com/25608527/83812009-6b34f180-a6d8-11ea-9f31-93d838d11895.png)
![38](https://user-images.githubusercontent.com/25608527/83812007-6a9c5b00-a6d8-11ea-98fb-a69f9d446e50.png)
![39](https://user-images.githubusercontent.com/25608527/83812046-76881d00-a6d8-11ea-9a98-0ee8cc7326dd.png)
![40](https://user-images.githubusercontent.com/25608527/83812038-7556f000-a6d8-11ea-8b09-e656e458ab86.png)
![41](https://user-images.githubusercontent.com/25608527/83812033-7425c300-a6d8-11ea-8c67-48c6d826cd3f.png)
![42](https://user-images.githubusercontent.com/25608527/83812083-8869c000-a6d8-11ea-8540-282ef444f964.png)
![43](https://user-images.githubusercontent.com/25608527/83812079-869ffc80-a6d8-11ea-8a6e-46a509970687.png)


