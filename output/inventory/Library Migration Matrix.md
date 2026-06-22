# Library Migration Matrix

전자정부프레임워크 3.1 → 4.3 전환 시 사용 라이브러리의 전환 대상 여부를 정리한 문서이다.

## 분류 기준

| 구분   | 설명                        |
| ---- | ------------------------- |
| 유지   | 그대로 사용 가능                 |
| 버전업  | 최신 버전으로 업그레이드             |
| 대체   | 다른 라이브러리 또는 프레임워크 기능으로 교체 |
| 제거   | 사용 중단                     |
| 검토   | 별도 분석 필요                  |
| 대상아님 | 전환 대상 아님                  |

## Library Matrix

|  NO | eGov 3.1 Lib                               | 구분          | 용도             | 전환대상 | eGov 4.3 Lib                     | 비고                |
| --: | ------------------------------------------ | ----------- | -------------- | ---- | -------------------------------- |  ---------------- |
|   1 | antlr-2.7.7.jar                            | Utility     | Parser         | 대상아님 | N/A                               | Hibernate 종속으로 유지(org.hibernate:hibernate-core:jar:5.6.15.Final) |
|   2 | antlr-3.5.jar                              | Utility     | Parser         | 검토  |                         | 사용처 확인 후 유지/제거 판단 |
|   3 | antlr-runtime-3.5.jar                      | Utility     | Parser Runtime | 검토  |                          | 사용처 확인 후 유지/제거 판단 |
|   4 | aopalliance-1.0.jar                        | Spring      | AOP            | 유지   | Spring Dependency                |
|   5 | aspectjweaver-1.8.0.jar                    | Spring      | AOP            | 버전업  | AspectJ                          | LTW 사용여부 확인 필요 (grep -R "load-time-weaver" .  grep -R "aop.xml" . grep -R "javaagent.*aspectjweaver" . grep -R "META-INF/aop.xml" . ) |
|   6 | bcprov-ext-jdk15-1.4.5.jar                 | Security    | 암호화            | 버전업  | BouncyCastle                     | 자동변환 어려움. org.bouncycastle:bcprov-ext-jdk18on:1.84 Maven 의존성으로 교체하는 것을 권장 |
|   7 | commons-1.0.jar                            | Utility     | Commons        | 검토   | 확인 필요                            |
|   8 | commons-beanutils-1.8.3.jar                | Utility     | Bean 처리        | 버전업  | Commons BeanUtils                |
|   9 | commons-collections-3.1.jar                | Utility     | Collection     | 버전업  | Commons Collections4             |
|  10 | commons-dbcp-1.4.jar                       | Persistence | DB Pool        | 대체   | HikariCP                         |
|  11 | commons-digester-1.8.jar                   | Utility     | XML Parsing    | 검토   | 확인 필요                            |
|  12 | commons-fileupload-1.3.1.jar               | Web         | 파일업로드          | 버전업  | Commons FileUpload               |
|  13 | commons-io-2.2.jar                         | Utility     | IO 처리          | 버전업  | Commons IO                       |
|  14 | commons-lang3-3.3.2.jar                    | Utility     | 문자열            | 버전업  | Commons Lang3                    |
|  15 | commons-logging-1.1.1.jar                  | Logging     | Logging        | 제거   | SLF4J/Logback                    |
|  16 | commons-net-3.3.jar                        | Utility     | FTP 등          | 버전업  | Commons Net                      |
|  17 | commons-pool-1.5.4.jar                     | Persistence | Pool           | 대체   | HikariCP                         |
|  18 | commons-validator-1.4.0.jar                | Validation  | 검증             | 유지   | Commons Validator                |
|  19 | egovframework.rte.fdl.cmmn-3.1.0.jar       | eGov        | 공통기능           | 대체   | org.egovframe.rte.fdl.cmmn       |
|  20 | egovframework.rte.fdl.idgnr-3.1.0.jar      | eGov        | ID 생성          | 대체   | org.egovframe.rte.fdl.idgnr      |
|  21 | egovframework.rte.fdl.logging-3.1.0.jar    | eGov        | 로깅             | 대체   | org.egovframe.rte.fdl.logging    |
|  22 | egovframework.rte.fdl.property-3.1.0.jar   | eGov        | Property       | 대체   | org.egovframe.rte.fdl.property   |
|  23 | egovframework.rte.psl.dataaccess-3.1.0.jar | eGov        | DAO            | 대체   | org.egovframe.rte.psl.dataaccess |
|  24 | egovframework.rte.ptl.mvc-3.1.0.jar        | eGov        | MVC            | 대체   | org.egovframe.rte.ptl.mvc        |
<<<<<<< HEAD
| 26 | `ibatis-sqlmap-2.3.4.726.jar` | Persistence | SQL Mapper | 대체 | `mybatis-3.5.x` + `mybatis-spring-2.1.x` / `org.egovframe.rte.psl.dataaccess` | iBatis 사용 범위 확인 후 MyBatis로 통합 전환 필요. `SqlMapClient`, `SqlMapClientTemplate`, `<sqlMap>`, `resultClass`, `parameterClass` 사용 여부 점검 |
| 27 | `icu4j-53.1.jar` | Utility | 국제화 / 문자 처리 | 버전업 | `icu4j` 최신 JDK8 호환 버전 | 유니코드, 로케일, 날짜/문자 처리용. 직접 사용 여부 확인 후 eGov 4.3 환경에서 호환 버전 적용 |
| 28 | `itext-2.1.7.jar` | Document | PDF 생성 / 편집 | 대체 | `OpenPDF 1.3.x` 또는 상용 `iText 7` | iText 3.x 이상은 AGPL 라이선스 이슈가 있어 공공기관은 OpenPDF 우선 검토 권장. OpenPDF는 `com.lowagie.text` 패키지 유지로 전환 부담 낮음 |
| 29 | `jackcess-2.0.7.jar` | Document / Data | MS Access 파일 처리 | 버전업 / 검토 | `jackcess` 최신 JDK8 호환 버전 | `.mdb`, `.accdb` 파일 사용 여부 확인. 실제 사용하지 않으면 제거 검토 가능 |
| 30 | `jackson-core-asl-1.9.13.jar` | JSON | JSON Core | 대체 | `com.fasterxml.jackson.core:jackson-core:2.x` | Jackson 1.x 계열에서 2.x 계열로 변경. `org.codehaus.jackson` → `com.fasterxml.jackson` import 변경 필요 |
| 31 | `jackson-mapper-asl-1.9.13.jar` | JSON | JSON Mapping | 대체 | `com.fasterxml.jackson.core:jackson-databind:2.x` + `jackson-annotations` | JSON ↔ Java 객체 매핑용. Spring MVC 설정에 `MappingJacksonHttpMessageConverter`가 있으면 `MappingJackson2HttpMessageConverter`로 변경 필요 |
| 32 | `jasypt-1.9.2.jar` | Security | 문자열 / Property 암호화 | 버전업 / 검토 | `jasypt-1.9.3` 또는 호환 설정 유지 | 암호화 알고리즘, 키 관리 방식, 운영 환경변수 관리 방식 확인 필요. 암호화/복호화 회귀 테스트 필수 |
| 33 | `jasypt-spring3-1.9.2.jar` | Security / Spring | Spring 암호화 연계 | 대체 / 검토 | `jasypt-spring31` 수동 Bean 설정 또는 Spring Boot 전환 시 `jasypt-spring-boot` | Jasypt 공식 1.9.x 라인에는 Spring 5 전용 모듈이 없음. XML 기반 Spring MVC 환경에서는 수동 Bean 설정 방식 검토 |
| 34 | `jcaos-client-arccert-1.4.7.1.jar` | Security | 인증서 / GPKI 추정 | 검토 | 공급사 최신 JDK8/WAS 호환 버전 | 사설/국산 인증서 모듈 가능성. GPKI, 인증서 로그인, ActiveX 제거 영향, 폐쇄망 반입 파일, 라이선스 확인 필요 |
| 35 | `jcl-over-slf4j-1.7.7.jar` | Logging | Commons Logging → SLF4J Bridge | 버전업 | `jcl-over-slf4j-1.7.36` 또는 eGov 4.3 검증 버전 | Commons Logging 호출을 SLF4J로 전달. `commons-logging.jar`와 중복 구성 여부 확인 필요 |
| 36 | `jdbc-14.jar` | Persistence | Oracle JDBC 추정 | 대체 / 검토 | `ojdbc8` 단일 적용 | `ojdbc14-10.2.0.1.0.jar`와 중복 가능성 큼. JAR Manifest 확인 후 Oracle JDBC 드라이버는 하나로 정리 필요 |
| 37 | `jdom-1.0.jar` | XML | XML 처리 | 대체 / 버전업 | `org.jdom:jdom2:2.x` | JDOM 1.x → JDOM2 전환 시 패키지와 API 변경 가능. XML 생성/파싱 사용 소스 확인 필요 |
| 38 | `jsch-0.1.54.jar` | Network | SSH / SFTP | 대체 / 버전업 | `com.github.mwiede:jsch:0.2.x` 또는 대체 라이브러리 | 원본 JCraft JSch는 유지보수가 제한적이므로 mwiede fork 검토. SFTP 업로드/다운로드, 암호화 알고리즘 호환성 테스트 필요 |
| 39 | `jstl-1.2.jar` | Web | JSTL API | 유지 / 검토 | `javax.servlet:jstl:1.2` 또는 WAS 기준 JSTL 구성 | eGovFrame 4.3 기본은 `javax.*` 유지. Tomcat 10/Servlet 5 이상이 아니면 `jakarta.*`로 일괄 전환하지 않음. WAS 내장 JSTL과 중복 확인 |
| 40 | `jta-1.1.jar` | Transaction | JTA API | 검토 | WAS 제공 JTA 또는 `javax.transaction-api` 계열 | JEUS/WebLogic 등 상용 WAS는 JTA를 제공할 수 있음. 단일 DB 트랜잭션은 Spring `DataSourceTransactionManager`로 처리 가능 여부 확인 |
| 41 | `lib.dstspdfSig-1.1.jar` | Security / Document | PDF 전자서명 추정 | 검토 | 공급사 최신 JDK8/WAS 호환 버전 | PDF 전자서명 모듈 가능성. 인증서, TSA, PDF 생성 라이브러리와 연계되므로 공급사 확인 및 업무 테스트 필수 |
| 42 | `lib.magic.tsaclient-1.1.jar` | Security | TSA 타임스탬프 클라이언트 추정 | 검토 | 공급사 최신 JDK8/WAS 호환 버전 | 타임스탬프 서버 연계 모듈 가능성. TSA 서버 주소, 인증서, 네트워크 정책, 공급사 API 변경 여부 확인 필요 |
| 43 | `log4j-api-2.3.2.jar` | Logging | Log4j2 API | 버전업 / 보안 | `log4j-api-2.17.1` 이상 또는 eGov 4.3 검증 버전 | Log4j 2.3.x는 보안 취약점 대상. `log4j-core`, `log4j-slf4j-impl`과 동일 버전 계열로 통일 필요 |
| 44 | `log4j-core-2.3.2.jar` | Logging | Log4j2 Core | 버전업 / 보안 | `log4j-core-2.17.1` 이상 또는 eGov 4.3 검증 버전 | Log4Shell 등 보안 취약점 조치 대상. 마이그레이션과 별개로 선제 패치 필요 |
| 45 | `log4j-over-slf4j-1.7.7.jar` | Logging | Log4j 1.x → SLF4J Bridge | 버전업 / 검토 | `log4j-over-slf4j-1.7.36` 또는 eGov 4.3 검증 버전 | 소스에서 `org.apache.log4j.Logger`를 직접 사용하면 필요. 직접 사용이 없으면 제거 검토 가능 |
| 46 | `log4j-slf4j-impl-2.3.1.jar` | Logging | SLF4J → Log4j2 Binding | 버전업 / 보안 | `log4j-slf4j-impl-2.17.1+` 또는 eGov 4.3 검증 버전 | `log4j-api/core`와 버전 통일 필요. `log4j-to-slf4j`와 동시 사용하면 순환 의존성 발생 가능 |
| 47 | `mail-1.4.jar` | Mail | 이메일 송수신 | 버전업 / 검토 | `javax.mail-1.6.x` 계열 | eGovFrame 4.3 기본 환경에서는 `javax.mail` 유지 검토. Tomcat 10/Servlet 5 이상이 아니면 `jakarta.mail` 전환은 별도 과제 |
| 48 | `mybatis-3.2.7.jar` | Persistence | SQL Mapper | 버전업 | `mybatis-3.5.x` | Spring 5 호환을 위해 `mybatis-spring-2.1.x`와 세트 업그레이드 필요. iBatis 잔존 영역과 통합 기준 수립 |
| 49 | `mybatis-spring-1.2.2.jar` | Persistence | MyBatis-Spring 연계 | 버전업 | `mybatis-spring-2.1.x` | Spring 5 호환 버전 필요. MyBatis 3.5.x 이상과 함께 적용하고 `SqlSessionFactoryBean`, `MapperScannerConfigurer` 설정 확인 |
| 50 | `ojdbc14-10.2.0.1.0.jar` | Persistence | Oracle JDBC Driver | 대체 | `ojdbc8` 단일 적용 | JDK8 기준 `ojdbc8`로 정리 권장. `jdbc-14.jar`와 중복 제거, DB/WAS 공통 lib 중복 확인, 드라이버 클래스 `oracle.jdbc.OracleDriver` 적용 확인 |
| ... | ...                                        | ...         | ...            | ...  | ...                              |
|  73 | xecure-7.jar                               | Security    | 전자서명           | 검토   | Non-ActiveX 대체                   |
=======
| 25 | ehcache-core-2.x.jar                       | Cache       | 캐시             | 버전업  | Ehcache 3.x                      |
| 26 | gson-2.2.x.jar                             | JSON        | JSON 처리        | 버전업  | Gson 최신                          |
| 27 | httpclient-4.3.x.jar                       | Network     | HTTP 통신        | 버전업  | HttpClient 5.x                   |
| 28 | httpcore-4.3.x.jar                         | Network     | HTTP Core      | 버전업  | HttpCore 5.x                     |
| 29 | ibatis-2.3.x.jar                           | Persistence | ORM            | 대체   | MyBatis 3.x                      |
| 30 | jackson-core-asl-1.x.jar                   | JSON        | JSON 처리        | 대체   | Jackson 2.x                      |
| 31 | jackson-mapper-asl-1.x.jar                 | JSON        | JSON Mapping   | 대체   | Jackson Databind                 |
| 32 | javassist-3.x.jar                          | Utility     | Bytecode       | 버전업  | Javassist 최신                     |
| 33 | jcl-over-slf4j.jar                         | Logging     | Logging Bridge | 유지   | SLF4J                            |
| 34 | jdom-1.x.jar                               | XML         | XML 처리         | 검토   | JDOM2                            |
| 35 | jedis-2.x.jar                              | Cache       | Redis          | 버전업  | Jedis 최신                         |
| 36 | jsch-0.1.x.jar                             | Network     | SSH/SFTP       | 버전업  | JSch 최신                          |
| 37 | json-lib-2.x.jar                           | JSON        | JSON 처리        | 대체   | Jackson/Gson                     |
| 38 | junit-4.x.jar                              | Test        | 단위테스트          | 버전업  | JUnit 5                          |
| 39 | log4j-1.2.x.jar                            | Logging     | Logging        | 제거   | Logback                          |
| 40 | log4jdbc-1.2.jar                           | Logging     | SQL Logging    | 검토   | log4jdbc-remix                   |
| 41 | mybatis-3.x.jar                            | Persistence | ORM            | 유지   | MyBatis 최신                       |
| 42 | mybatis-spring-1.x.jar                     | Persistence | Spring 연동      | 버전업  | MyBatis-Spring 3.x               |
| 43 | ojdbc6.jar                                 | Database    | Oracle JDBC    | 버전업  | ojdbc11.jar                      |
| 44 | poi-3.x.jar                                | Office      | Excel 처리       | 버전업  | Apache POI 최신                    |
| 45 | poi-ooxml-3.x.jar                          | Office      | Excel OOXML    | 버전업  | Apache POI 최신                    |
| 46 | quartz-2.x.jar                             | Batch       | Scheduler      | 유지   | Quartz 최신                        |
| 47 | slf4j-api-1.7.x.jar                        | Logging     | Logging API    | 버전업  | SLF4J 2.x                        |
| 48 | slf4j-log4j12-1.7.x.jar                    | Logging     | Log4j 연동       | 제거   | Logback                          |
| 49 | spring-aop-4.0.x.jar                       | Spring      | AOP            | 버전업  | Spring 6.x                       |
| 50 | spring-beans-4.0.x.jar                     | Spring      | Bean 관리        | 버전업  | Spring 6.x                       |
| 51 | spring-context-4.0.x.jar                   | Spring      | Context        | 버전업  | Spring 6.x                       |
| 52 | spring-core-4.0.x.jar                      | Spring      | Core           | 버전업  | Spring 6.x                       |
| 53 | spring-expression-4.0.x.jar                | Spring      | SpEL           | 버전업  | Spring 6.x                       |
| 54 | spring-jdbc-4.0.x.jar                      | Spring      | JDBC           | 버전업  | Spring 6.x                       |
| 55 | spring-tx-4.0.x.jar                        | Spring      | Transaction    | 버전업  | Spring 6.x                       |
| 56 | spring-web-4.0.x.jar                       | Spring      | Web            | 버전업  | Spring 6.x                       |
| 57 | spring-webmvc-4.0.x.jar                    | Spring      | MVC            | 버전업  | Spring 6.x                       |
| 58 | taglibs-standard-1.1.x.jar                 | Web         | JSTL           | 대체   | jakarta.servlet.jsp.jstl         |
| 59 | tiles-api-2.x.jar                          | Web         | 화면구성           | 제거   | Thymeleaf                        |
| 60 | tiles-core-2.x.jar                         | Web         | 화면구성           | 제거   | Thymeleaf                        |
| 61 | tiles-jsp-2.x.jar                          | Web         | 화면구성           | 제거   | Thymeleaf                        |
| 62 | velocity-1.7.jar                           | Template    | 템플릿 엔진         | 제거   | Thymeleaf                        |
| 63 | xalan-2.x.jar                              | XML         | XSLT           | 검토   | JDK 기본                           |
| 64 | xercesImpl-2.x.jar                         | XML         | XML Parser     | 검토   | JDK 기본                           |
| 65 | xml-apis-1.x.jar                           | XML         | XML API        | 제거   | JDK 기본                           |
| 66 | xmlbeans-2.x.jar                           | XML         | XML Binding    | 버전업  | XMLBeans 최신                      |
| 67 | activation-1.1.jar                         | Jakarta     | Mail 지원        | 대체   | jakarta.activation               |
| 68 | mail-1.4.x.jar                             | Jakarta     | 메일             | 대체   | jakarta.mail                     |
| 69 | servlet-api-2.5.jar                        | Web         | Servlet API    | 대체   | jakarta.servlet-api              |
| 70 | jsp-api-2.1.jar                            | Web         | JSP API        | 대체   | jakarta.servlet.jsp-api          |
| 71 | standard.jar                               | Web         | JSTL           | 대체   | jakarta.servlet.jsp.jstl         |
| 72 | validator-rules.xml 관련 라이브러리               | Validation  | 입력값 검증         | 유지   | Commons Validator                |
| 73 | xecure-7.jar                               | Security    | 전자서명           | 검토   | Non-ActiveX 대체                   |
>>>>>>> upstream/main
