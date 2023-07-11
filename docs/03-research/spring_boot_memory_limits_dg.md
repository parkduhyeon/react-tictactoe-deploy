# Spring Boot 메모리 제한 적용 방법
## Spring Boot 메모리 제한을 걸어야 하는 이유
- 애플리케이션 실행 중 예상치 못한 메모리 부족 현상(OutOfMemoryErrors) 등을 방지하기 위함.
- 자원 관리를 효율적으로 수행하기 위함.
## Spring Boot 메모리 제한 방식
Spring Boot 애플리케이션에 메모리 제한을 걸기 위해서는 **Spring Boot 내 설정을 통해 진행하지 못하고, JVM 설정을 통해서만 가능하다.** 다음과 같은 방법이 존재한다.
### Heap 메모리 할당 및 제한
Heap 메모리는 Java에서 객체를 저장하는 공간이다. 해당 공간을 제한하는 cli 명령어는 다음과 같다.
- `-Xms`: initial 메모리 용량 선언.
  - ex) `java -Xms512m -jar <애플리케이션.jar>`: Heap 메모리의 초기 용량을 512MB로 할당한다.
- `-Xmx`: maximum 메모리 용량 선언.
  - ex) `java -Xmx2g -jar <애플리케이션.jar>`: Heap 메모리의 최대 용량을 2GB로 제한한다.
- 두 옵션을 동시에 적용할 수 있다.
  - ex) `java -Xms512m -Xmx2g -jar <애플리케이션.jar>`: Heap 메모리의 초기 용량을 512MB로 할당하고, 최대 용량을 2GB로 제한한다.
### JVM 전체 메모리 할당량을 물리적 RAM 용량에 % 비율로 메모리 할당 및 제한
JVM 전체 메모리는 heap 영역과 non-heap 영역 모두를 포함한다.  
- `-XX:MinRAMPercentage`: RAM 메모리 최소 할당률.
  - ex) `java -XX:MinRAMPercentage=25.0 -jar <애플리케이션.jar>`: RAM 메모리의 25%를 JVM 전체 메모리의 영역으로 할당한다.
- `-XX:MaxRAMPercentage`: RAM 메모리 최대 할당률.
  - ex) `java -XX:MaxRAMPercentage=75.0 -jar <애플리케이션.jar>`: RAM 메모리의 75%를 JVM 전체 메모리의 최대 용량으로 제한한다.
- 마찬가지로, 두 옵션은 동시에 적용이 가능하다.
### JVM 전체 메모리 할당량을 명확한 수치로 할당 및 제한
마찬가지로, JVM 전체 메모리는 heap 영역과 non-heap 영역 모두를 포함한다.
- `-XX:InitialRAMSize`: JVM 메모리 초기 할당량.
  - ex) `java -XX:InitialRAMSize=256m -jar <애플리케이션.jar>`: JVM 메모리 초기 할당량을 256MB로 할당한다.
- `-XX:MaxRAMSize`: JVM 메모리 최대 할당량 제한.
  - ex) `java -XX:MaxRAMSize=1g -jar <애플리케이션.jar>`: JVM 메모리 최대 할당량을 1GB로 제한한다.