# Todo Web Application using Spring Boot and H2 In memory database

Run com.bunny.springboot.web.SpringBootFirstWebApplication as a Java Application.

Runs on default port of Spring Boot - 8080 

## Can be run as a Jar or a WAR

`mvn clean install` generate a war which can deployed to your favorite web server.

We will deploy to Cloud as a WAR

## Web Application

- http://localhost:8080/login with Devil/dummy as credentials
- You can add, delete and update your todos
- Spring Security is used to secure the application
- `com.bunny.springboot.web.security.SecurityConfiguration` contains the in memory security credential configuration.

## H2 Console

- http://localhost:8080/h2-console
- Use `jdbc:h2:mem:testdb` as JDBC URL 


![](https://user-images.githubusercontent.com/25608527/83552197-01291a80-a527-11ea-91a8-5b6432070e50.png)

![](https://user-images.githubusercontent.com/25608527/83552200-01c1b100-a527-11ea-8e99-a81059aeea69.png)

![](https://user-images.githubusercontent.com/25608527/83552201-02f2de00-a527-11ea-9974-af4b84ab5675.png)

![](https://user-images.githubusercontent.com/25608527/83552205-038b7480-a527-11ea-8896-bf85406fd0ab.png)

![](https://user-images.githubusercontent.com/25608527/83552207-04bca180-a527-11ea-9042-b8910318b3c1.png)

![](https://user-images.githubusercontent.com/25608527/83552213-05edce80-a527-11ea-9b2b-032995854980.png)

![](https://user-images.githubusercontent.com/25608527/83552217-07b79200-a527-11ea-8e43-d6cdbb07ce68.png)

![](https://user-images.githubusercontent.com/25608527/83552228-0a19ec00-a527-11ea-9e98-dae60dbe9036.png)

![](https://user-images.githubusercontent.com/25608527/83552232-0b4b1900-a527-11ea-90d8-af8d3293c6c2.png)

![](https://user-images.githubusercontent.com/25608527/83552237-0e460980-a527-11ea-9d5c-f42e373eb645.png)

![](https://user-images.githubusercontent.com/25608527/83552240-0f773680-a527-11ea-83d9-09d602502af6.png)
