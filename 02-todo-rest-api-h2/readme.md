# Todo and Hello World Rest APIs Connecting to H2 In memory database running on port 5000

Run com.bunny.rest.webservices.restfulwebservices.RestfulWebServicesApplication as a Java Application.


## Hello World Resource

- http://localhost:5000/hello-world

```txt
Hello World
```

- http://localhost:5000/hello-world-bean

```json
{"message":"Hello World - Changed"}
```

- http://localhost:5000/hello-world/path-variable/Devil

```json
{"message":"Hello World, Devil"}
```


## Todo Resource

- GET - http://localhost:5000/jpa/users/Kalpesh/todos

```
[
  {
    "id": 10001,
    "username": "Kalpesh",
    "description": "Learn JPA",
    "targetDate": "2019-06-27T06:30:30.696+0000",
    "done": false
  },
  {
    "id": 10002,
    "username": "Devil",
    "description": "Learn Data JPA",
    "targetDate": "2019-06-27T06:30:30.700+0000",
    "done": false
  },
  {
    "id": 10003,
    "username": "Bunny",
    "description": "Learn Microservices",
    "targetDate": "2019-06-27T06:30:30.701+0000",
    "done": false
  }
]
```

#### Retrieve a specific todo

- GET - http://localhost:5000/jpa/users/Kalpesh/todos/10001

```
{
  "id": 10001,
  "username": "Kalpesh",
  "description": "Learn JPA",
  "targetDate": "2019-06-27T06:30:30.696+0000",
  "done": false
}
```

#### Creating a new todo



- POST to http://localhost:5000/jpa/users/Boss/todos with BODY of Request given below

```
{
  "username": "Boss",
  "description": "Learn to Drive a Car",
  "targetDate": "2030-11-09T10:49:23.566+0000",
  "done": false
}
```

#### Updating an existing todo

- PUT Request to http://localhost:5000/jpa/users/Kalpesh/todos/10001 with BODY of Request given below

```
{
  "id": 10001,
  "username": "Kalpesh",
  "description": "Learn to Drive a Car",
  "targetDate": "2045-11-09T10:49:23.566+0000",
  "done": false
}
```

#### Delete todo

- DELETE to http://localhost:5000/jpa/users/Kalpesh/todos/10001


## H2 Console

- http://localhost:5000/h2-console
- Use `jdbc:h2:mem:testdb` as JDBC URL 


## Build Spec for AWS Code Pipeline
```
version: 0.2
            
phases:
  install:
    runtime-versions:
      java: openjdk8
    commands:
      - echo install
  pre_build:
    commands:
      - echo pre_build
  build:
    commands:
      - mvn package
      - echo build
  post_build:
    commands:
      - echo post_build

artifacts:
  files:
    - target/spring-boot-todo-rest-api-h2-aws-codepipeline-0.0.1-SNAPSHOT.jar
```



![](https://user-images.githubusercontent.com/25608527/83551708-56186100-a526-11ea-9a61-b3bfef8a2ddc.png)

![](https://user-images.githubusercontent.com/25608527/83551710-56b0f780-a526-11ea-87cb-8071795efad6.png)

![](https://user-images.githubusercontent.com/25608527/83551712-57e22480-a526-11ea-85d3-abfa3db6983f.png)

![](https://user-images.githubusercontent.com/25608527/83551716-59135180-a526-11ea-905b-478ded0302ac.png)

![](https://user-images.githubusercontent.com/25608527/83551723-59abe800-a526-11ea-8e4e-4493ab1b0004.png)

![](https://user-images.githubusercontent.com/25608527/83551836-865fff80-a526-11ea-9851-d0c0f3b296b5.png)

![](https://user-images.githubusercontent.com/25608527/83551841-87912c80-a526-11ea-805f-2363b85e947d.png)

![](https://user-images.githubusercontent.com/25608527/83551870-8cee7700-a526-11ea-916c-1034789f08d7.png)

![](https://user-images.githubusercontent.com/25608527/83551885-8fe96780-a526-11ea-8eb7-78ad3c17db2a.png)

![](https://user-images.githubusercontent.com/25608527/83551898-91b32b00-a526-11ea-9e7d-a3c06896d4bc.png)

![](https://user-images.githubusercontent.com/25608527/83551920-95df4880-a526-11ea-9b2c-ae91fa3eb699.png)

![](https://user-images.githubusercontent.com/25608527/83551929-98da3900-a526-11ea-9f3d-d60cee802041.png)

![](https://user-images.githubusercontent.com/25608527/83551934-9aa3fc80-a526-11ea-8246-ce9dad72b30e.png)

![](https://user-images.githubusercontent.com/25608527/83551941-9c6dc000-a526-11ea-93e3-f7b6d18e9f85.png)

![](https://user-images.githubusercontent.com/25608527/83551943-9d9eed00-a526-11ea-8f32-6fdf95745370.png)

![](https://user-images.githubusercontent.com/25608527/83551948-9ed01a00-a526-11ea-804c-af9bb501a3b4.png)

![](https://user-images.githubusercontent.com/25608527/83551950-a099dd80-a526-11ea-9961-1b7ed04fe4f4.png)

![](https://user-images.githubusercontent.com/25608527/83551952-a1cb0a80-a526-11ea-9dca-6980d75c19b4.png)

![](https://user-images.githubusercontent.com/25608527/83551954-a2fc3780-a526-11ea-8e6c-5a0dc1c6a136.png)

![](https://user-images.githubusercontent.com/25608527/83551956-a394ce00-a526-11ea-93f8-b99985a795ef.png)
