[소스코드](https://github.com/taehvvan/hotel-reservation)


## Visual Studio Code와 MariaDB 연동 방법

### 1. MariaDB 설치
1. [MariaDB 공식 홈페이지](https://mariadb.org/download/?t=mariadb&p=mariadb&r=12.0.2&os=windows&cpu=x86_64&pkg=msi&mirror=blendbyte)에서 설치 파일 다운로드
2. 설치 파일 실행 -> 계정명은 root, 패스워드는 1234로 설정
3. `mysql -u root -p` 명령어로 접속 확인

### 2. 시스템 환경 변수 설정
1. 시스템 환경 변수 설정으로 이동
2. 시스템 변수에서 Path 편집
3. MariaDB 설치 경로 추가
> (예시) C:\Program Files\MariaDB 12.0\bin

### 3. pom.xml에 MariaDB 드라이버 추가
```xml
<dependency>
  <groupId>org.mariadb.jdbc</groupId>
  <artifactId>mariadb-java-client</artifactId>
  <version>3.3.2</version> <!-- 최신버전 확인 필요 -->
</dependency>
```

### 4. application.properties 설정
```properties
# DB 연결 정보 (db명은 필요 시 수정)
spring.datasource.url=jdbc:mariadb://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=1234
spring.datasource.driver-class-name=org.mariadb.jdbc.Driver

# (선택) JPA 사용 시
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```
