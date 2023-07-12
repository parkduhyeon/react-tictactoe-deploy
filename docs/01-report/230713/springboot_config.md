### Spring Boot 내 application.yml 설정

## application.yml
- src/main/resources 폴더 경로에 위치
- Spring Boot 설정 전반에 반영되는 파일이다
- 처음 프로젝트 생성 시 application.properties 파일이 위치 
- 가독성 면에서 더 나은 YAML 파일 형식인 application.yml로 작성을 하는 것을 선호.  

### application 작성 설정 종류

application.properties

```properties
server.port = 5000
```

- application.yml
1. server port 지정.

```yaml
server:
    port: 5000
```

해당 정보를 기입하면 내장된 Tomcat 서버의 포트가 5000으로 변경된다. 미기재시 8080이 default 포트로 지정된다.  


![Alt text](./img/port5000.png)
![Alt text](./img/port_page.png)

1. database 설정.  
Spring Boot로 구현하는 백 서버의 경우 대다수가 데이터베이스에 접근하는 구조로 되어 있다. 해당 데이터베이스 접근 예시는 다음과 같다(MySQL).
```yaml
spring:
    datasource:
        url: jdbc:mysql://localhost:3306/mydatabase
        username: myusername
        password: mypassword
        driver-class-name: com.mysql.jdbc.Driver
```
1. 각종 Swagger/OpenAPI, spring security, hibernate, OAuth 설정 등 다방면에서 설정을 진행할 수 있다.
2. 환경변수를 지정하여 애플리케이션 내에 노출하지 않도록 필터 처리를 진행할 수 있다.