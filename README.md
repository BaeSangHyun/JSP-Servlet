# JSP-Servlet

## Content
- [웹프로그래밍이란](#웹프로그래밍이란)
- [Java Web](#java-web)
- [Servlet](#servlet)
    - [Servlet Mapping](#servlet-mapping)
        - [Servlet Mapping 방법](#servlet-mapping-방법)
    - [doGet(), doPost()](#doget-dopost)
    - [Context Path](#context-path)
    - [Servlet 작동순서](#servlet-작동순서)
    - [Servlet LifeCyle](#servlet-lifecyle)
    - [Servlet 선,후처리](#servlet-선후처리)
    - [Servlet Parameter](#servlet-parameter)
    - [한글 Encoding](#한글-encoding)
    - [Servlet 초기화 파라미터](#servlet-초기화-파라미터)
    - [데이터 공유](#데이터-공유)
    - [웹어플리케이션 감시](#웹어플리케이션-감시)
- [JSP](#jsp)
    - [JSP 태그종류](#jsp-태그종류)
    - [JSP 동작원리](#jsp-동작원리)
    - [JSP 내부 객체](#jsp-내부-객체)
        - [내부 객체 종류](#내부-객체-종류)
    - [문법](#문법)
        - [Script](#script)
        - [지시자](#지시자)
        - [주석](#주석)
    - [Request 객체](#request-객체)
        - [Request객체 관련 메소드](#request객체-관련-메소드)
        - [Parameter 메소드](#parameter-메소드)
    - [Response 객체](#response-객체)
        - [Response객체 관련 메소드](#response객체-관련-메소드)
    - [Action 태그](#Action-태그)
    - [쿠키](#쿠키)
    - [세션](#세션)
        -[세션 메소드](#세션-메소드)

## 1. 웹프로그래밍이란
1. 웹프로그래밍이란, 웹어플리케이션을 구현하는 행위
2. 웹어플리케이션이란, 웹을 기반으로 작동되는 프로그램
3. 웹이란, 1개 이상의 사이트가 연결되어있는 인터넷 서비스의 한가지 형태
4. 인터넷이란, 1개 이상의 네트워크가 연결되어 있는 형태

- 프로토콜(Protocol) : 네트워크상에서 약속한 통신규약(Http, FTP, SMTP, POP, DHCP)(Default 값이 Http 이므로 Http 프로토콜을 사용할 시 생략해도 된다.))
- IP : 네트워크상에서 컴퓨터를 식별할 수 있는 주소
- DNS : IP주소를 인간이  외우도록 맵핑한 문자열
- Port : IP주소가 컴퓨터를 식별할 수 있게 해준다면, Port번호는 해당컴퓨터의 구동되고 있는 프로그램을 구분할 수 있는 번호(Default 값이 있으므로 생략해도 된다.)

### 예시

<table>
    <tr>
        <th colspan="4">http://www.sba.seoul.kr:80/kr/index</th>
    </tr>
    <tr>
        <td>http</td><td>www.sba.seoul.kr</td><td>80</td><td>kr/index</td>
    </tr>
    <tr>
        <td>프로토콜</td><td>컴퓨터 주소(DNS를 통한 IP주소로 변경)</td><td>port</td><td>information path</td>
    </tr>
</table>

## 2. Java Web
JAVA플랫폼(J2SE, J2EE, J2ME)중에서 J2EE를 이용한 웹프로그래밍
![web](https://user-images.githubusercontent.com/42559714/44499590-83807b80-a6bf-11e8-8ee9-933083dd6405.PNG)

## 3. Servlet

### Servlet Mapping
- 접속 경로가 너무 긴 경우 짧은 이름으로 사용할 수 있습니다.
- 보안에 노출되어 있는 경로를 다른 이름으로 간단하게 맵핑할 수 있습니다.

<table>
    <tr>
        <th>기존경로</th><td>http://localhost:8080/HelloWorld/servlet/com.javalec.ex.HelloWorld</td>
    </tr>
    <tr>
        <th>URL맵핑 경로</th><td>http://localhost:8080/HelloWorld/HW</td>
    </tr>
</table>

#### Servlet Mapping 방법
- [Annotation을 이용한 서블릿 맵핑](http://codedragon.tistory.com/4596)

- [web.xml에 서블릿 맵핑](http://codedragon.tistory.com/4604)

- [Annotation과 XML의 차이점](http://blog.naver.com/PostView.nhn?blogId=wwwkang8&logNo=220994093310)

### doGet(), doPost()

#### doGet(),doPost() 구문
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub	
	}

protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
	}
```

### Context Path
WAS에서 웹어플리케이션을 구분하기 위한 path.
이클립스에서 프로젝트를 생성하면 자동으로 server.xml에 생성된다.

### Servlet 작동순서

![3](https://user-images.githubusercontent.com/42559714/44635072-21d05200-a9dc-11e8-832b-ea051f881575.PNG)
요청이 있을 때마다 쓰레드를 생성하여 처리하기 때문에 서버부하가 적다.

### Servlet LifeCycle
Servelt은 최초 요청 시 객체가 만들어져 메모리에 로딩되고, 이후 요청 시에는 만들었던 객체를 재활용하여 동작속도가 빠르다.

![4](https://user-images.githubusercontent.com/42559714/44635201-732d1100-a9dd-11e8-9271-9aafe5fb5702.PNG)

### Servlet 선,후처리
LifeCycle 중 init()과 destroy()메소드에 관련하여 선처리(init)와 후처리(destroy) 작업이 가능하다.

![5](https://user-images.githubusercontent.com/42559714/44635240-c1421480-a9dd-11e8-90e2-39a9978ae9af.PNG)

### Servlet Parameter
Form 태그의 submit 버튼을 클릭하여 데이터를 서버로 전송 후 해당파일에서 HttpServletRequest객체를 사용하여 Parameter값을 얻을 수 있다.

![6](https://user-images.githubusercontent.com/42559714/44635273-20a02480-a9de-11e8-8887-58121b24dab0.PNG)

### 한글 Endocing
서버마다 문자 처리방식이 다르기 때문에 개발자가 별도의 한글 인코딩을 해주지 않으면 한글이 꺠져보이는 현상이 있다.

![7](https://user-images.githubusercontent.com/42559714/44635393-fcddde00-a9df-11e8-876a-0dab5de4dfb8.PNG)

### Servlet 초기화 파라미터
특정 Servlet이 생성될때 특정 경로 및 아이디 정보 등 초기에 플요한 데이터들이 있다.
이런 데이터들을 초기화 파라미터라고 하며, web.xml에 기술하거나 Servlet파일에 직접 기술하여 `ServletConfig 클래스`를 이용하여 사용한다.

#### web.xml파일에 초기화 파라미터 기술

![8](https://user-images.githubusercontent.com/42559714/44635517-06b41100-a9e1-11e8-981a-ab64325852ba.PNG)

#### Servlet파일에 초기화 파라미터 기술

![9](https://user-images.githubusercontent.com/42559714/44635519-07e53e00-a9e1-11e8-917f-f3d886ab3fc1.PNG)

### 데이터 공유
여러 Servlet에 특정 데이터를 공유해야 할 경우 `context parameter`를 이용하여 web.xml에 기술하고 Servlet에서 공유해서 사용할 수 있다.

![10](https://user-images.githubusercontent.com/42559714/44635565-58f53200-a9e1-11e8-97f7-bcb06ec9dd4b.PNG)

### 웹어플리케이션 감시
`ServletContextListener` 클래스는 웹 어플리케이션 생명주기(LifeCycle)을 감시하여 리스너의 해당 메소드가 웹 어플리케이션의 시작과 종료 시 호출된다.

![11](https://user-images.githubusercontent.com/42559714/44635626-e3d62c80-a9e1-11e8-9a8f-12d29068b1ae.PNG)



## 4. JSP

### JSP 태그종류
기능 | 코드 | 설명
:---:|:---:|:---:
지시자 | `<%@       %>` | 페이지 속성
주석 | `<%--      --%>` |
선언 | `<%!         %>` | 변수, 메소드 선언
표현식 | `<%=       %>` | 결과값 출력
스크립트릿 | `<%    %>` | JAVA 코드
액션태그 | `<jsp:action>  </jsp:action>` | 자바빈 연결

### JSP 동작원리
- 클라이언트가 웹브라우저로 *.jsp를 요청하게되면 JSP컨테이너가 JSP파일을 Servlet파일(.java)로 변환한다. 그리고 Servlet파일(.java)은 컴파일 된 후 클래스 파일(.class)로 변환되고, 요청한 클라이언트한테 html파일 형태로 응답된다.
- 클라이언트가 jsp를 요청하면 Servlet이 있는지 없는지를 확인하고 없으면 Servlet을 생성하여 요청에 대한 응답을 하고 그 뒤로 생성했던 Servlet을 지속적으로 재활용하여 실행하므로 속도가 빠르다.
![1](https://user-images.githubusercontent.com/42559714/44564936-8c954980-a7a0-11e8-844f-5933b1c362e8.PNG)

### JSP 내부 객체
개발자가 객체를 생성하지 않고 바로 사용할 수 있는 객체<br />
JSP에서 제공되는 내부객체는 JSP컨테이너에 의해 Servlet으로 변화될 때 자동으로 객체가 생성된다.

#### 내부 객체 종류
객체선언을 할 필요가 없다.
- 입출력 객체 : `request`, `response`, `out`
- 서블릿 객체 : `page`, `config`
- 세션 객체 : `session`
- 예외 객체 : `exception`

### 기본 문법

#### Script
- 스크립트릿(scriptlet) : `<%  java 코드 기술  %>`
    - JSP페이지에서 JAVA언어를 사용하기 위한 요소
- 선언(declaration) : `<%  java 코드 기술  %>`
    - JSP페이지 내에서 사용되는 변수 또는 메소드를 선언할 때 사용
    - 선언된 변수 및 메소드는 전역의 의미로 사용된다.
- 표현식(expression) : `<%=  java 코드 기술  %>`
    - JSP페이지 내에서 사용되는 변수의 값 또는 메소드 호출 결과값을 출력하기 위해 사용
    - String 타입이며, ';'를 사용할 수 없다.

#### 지시자
`<%@    속성    %>`<br />
JSP페이지의 전체적인 속성을 지정할 때 사용

##### page 지시자
- 페이지의 속성을 지정할 때 사용. 주로 사용되는 언어 지정 및 import문을 많이 사용
```js
<%@page import="java.util.Arrays"%>
<%@page language="java" contentType="text/html; charset=EUC-KR" pageEncoding="EUC-KR"%>
```

##### include 지시자
- 현재 페이지내에 다른 페이지를 삽입 할 때 사용. file속성을 이용한다.
```js
<%@ include file="*.jsp"%>
```

#### 주석
`<!--  comment  -->`<br />
실제 프로그램에는 영향이 없고, 프로그램 설명들의 목적으로 사용되는 태그<br /><br />
JSP주석은 HTML과는 다르게 WAS에서 컴파일 후 응답하는 형식이라 주석된 부분은 브라우저 소스보기에서 보이지 않는다.

### Request 객체
`request` : 웹브라우저를 통해 서버에 어떤 정보를 요청하는 것

#### Request객체 관련 메소드
- `getContextPath()` : 웹어플리케이션의 컨텍스트 패스를 얻는다.
- `getMethod()` : get방식과 post방식을 구분할 수 있다.
- `getSession()` : 세션 객체를 얻는다.
- `getProtocol()` : 해당 프로토콜을 얻는다.
- `getRequestURL()` : 요청 URL을 얻는다.
- `getRequestURI()` : 요청 URI를 얻는다.
- `getQueryString()` : 쿼리스트링을 얻는다.

#### Parameter 메소드
- `getParameter(String name)` : name에 해당하는 파라미터 값을 구함
- `getParameterNames()` : 모든 파라미터 이름을 구함
- `getPrameterVvalues(String name)` : name에 해당하는 파라미터값들을 구함

### Response 객체
`reponse` : 웹브라우저의 요청에 응답하는 것

#### Response객체 관련 메소드
- `getCharacterEncoding()` : 응답할 때 문자의 인코딩 형태를 구한다.
- `addCookie(Cookie)` : 쿠키를 지정 한다.
- `sendRedirect(URL)` : 지정한 URL로 이동한다.


### Action 태그
JSP페이지 내에서 어떤 동작을 하도록 지시하는 태그.

- `foward` : 현재의 페이지에서 다른 특정페이지로 전환할 때 사용. `URL값은 그대로 남는다`.
```java
<jsp:forward page="*.jsp"/>
```

- `include` 태그
현재 페이지에 다른 페이지를 삽입할 때 사용한다. 삽입한 페이지를 다 실행 후 본래 페이지로 돌아와 마저 실행한다.
```java
<jsp:page="*.jsp" flush="true" />
```

- `param` 태그
forward 및 include 태그에 데이터 전달을 목적으로 사용되는 태그. 이름과 값으로 이루어져 있다.
```java
    <jsp:forward page="*.jsp">
        <jsp:param name="id" value="abcdef" />
        <jsp:param name="pw" value="1234" />
    </jsp:forward>
```

### 쿠키
> 웹브라우저에서 서버로 어떤 데이터를 요청하면, 서버측에서는 알맞은 로직을 수행한 수 데이터를 웹브라우저에 응답합니다. 그리고, 서버는 웹브라우저와의 관계를 종료합니다. 이렇게, 웹브라우저에 응답 후 관계를 끊는 것은 http프로토콜의 특징입니다.
연결이 끊겼을 때 어떤 정보를 지속적으로 유지하기 위한 수단으로 쿠키라는 방식을 사용합니다. **쿠키는 서버에서 생성하여, 서버가 아닌 클라이언트 측에 특정 정보를 저장**합니다. 그리고 서버에 요청 할 때 마다 속성값을 참조 또는 변경 할 수 있습니다.<br />
쿠키는 4kb로 용량이 제한적이며, 300개까지 데이터 정보를 가질 수 있습니다.

![2](https://user-images.githubusercontent.com/42559714/44571608-2fa78c80-a7bc-11e8-9fbc-0b0d710ce53d.PNG)

#### 쿠키 관련 메소드
- `setMaxAge()` : 쿠키 유효기간을 설정
- `setpath()` : 쿠키사용의 유효 디렉토리를 설정
- `setValue()` : 쿠키의 값을 설정
- `setVersion()` : 쿠키 버전을 설정
- `getMaxAge()` : 쿠키 유효기간 정보를 얻음
- `getName()` : 쿠키 이름을 얻음
- `getPath()` : 쿠키사용의 유효 디렉토리 정보를 얻음
- `getValue()` : 쿠키의 값을 얻음
- `getVersion()` : 쿠키 버전을 얻음

### 세션
쿠키와 마찬가지로 서버와의 관계를 유지하기 위한 수단.
쿠키와 달리 클라이언트의 특정 위치에 저장되는 것이 아니라, 서버상에 객체로 존재한다.
따라서 **세션은 서버에서만 접근이 가능하고 보안이 좋고, 저장할 수 있는 데이터 한계가 없다**.

![session](https://user-images.githubusercontent.com/42559714/44625044-cf3e5980-a939-11e8-9741-2c628866206b.PNG)

#### 세션 메소드
- `setAttribute()` : 세션에 데이터를 저장.
- `getAttribute()` : 세션에서 데이터를 얻는다. (Object로 받아진다.)
- `getAttributeNames()` : 세션에 저장되어 있는 모든 데이터의 이름(유니크한 키값)을 얻는다.
- `getId()` : 자동 생성된 세션의 유니크한 아이디를 얻는다.
- `isNew()` : 세션이 최초 생성되었는지, 이전에 생성된 세션인지를 구분.
- `getMaxInactiveInterval()` : 세션의 유효시간을 얻는다. 가장 최근 요청시점을 기준으로 카운트.(tomcat폴더의 conf\web.xml파일을 수정하면 세션의 유효시간을 설정 할 수 있다.)
- `removeAttribute()` : 세션에서 특정 데이트를 제거.
- `Invalidate()` : 세션의 모든 데이터를 삭제.

### 예외 페이지
#### 예외 발생 페이지
- `<%@ page errorPage="*.jsp"%>` : 현재 페이지에서 에러가 발생하면 특정 페이지로 이동하게 하는 커맨드
#### 예외 페이지
- `<%@ page isErrorPage="true"%>` : 기본값이 false 이므로 true로 명시를 해줘야 exception 객체를 사용할 수 있다.
- `<% response.setStatus(200); %>` : 예외 페이지는 에러가 발생된 페이지가 아니고 에러가 무엇인지를 보여주는 정상적인 페이지인데 200(정상)이라고 Status를 명시해주지 않으면 웹서버에서 전페이지의 에러코드에 대한 자체적으로 제공하는 페이지로 넘어가기 때문에 명시해줘야한다.
- `<%= exception.getMessage() %>` : 예외가 발생된 이유를 표시해준다.

### 자바 빈
반복적인 작업을 효율적으로 하기 위해 빈을 사용한다. 빈이란, JAVA언어의 데이터(속성)와 기능(메소드)으로 이루어진 클래스이다.
jsp페이지를 만들고, 액션태그를 이용하여 빈을 사용한다. 그리고 빈의 내부 데이터를 처리한다.

#### 관련 액션 태그
- `useBean` : 특정 Bean을 사용한다고 명시할 때 사용<br />
`<jsp:useBean id="Bean이름" class="패키지명.Bean이름" scope="page"/>`
    - `Scope`
        - `page` : 생성된 페이지 내에서만 사용 가능
        - `request` : 요청된 페이지 내에서만 사용 가능
        - `session` : 웹브라우저의 생명주기와 동일하게 사용 가능
        - `application` : 웹 어플리케이션 생명주기와 동일하게 사용 가능
- `setProperty` : 데이터 값을 설정할 때 사용<br />
`<jsp:setProperty name="Bean이름" property="속성이름" value="속석(데이터)값"/>`
- `getProperty` : 데이터 값을 가져올 때 사용<br />
`<jsp:getProperty name="Bean이름" property="속성이름">`

## 데이터베이스
체계화된 데이터의 모임이다. 즉, 작성된 목록으로써 여러 응용 시스템들의 통합된 정보들을 저장하여 운영할 수 있는 공용 데이터들의 묶음이다.

#### DBMS
**DBMS(DataBase Management System, 데이터 베이스 관리 시스템)**은 언어와 데이터 베이스를 연결해 주는 도구이다. 일반적으로 데이터 베이스와 동일시한다.
DBMS는 종류가 다양하며, 그중에서도 가장 많이 사용하는 것이 RDBMS(Relational DataBase Management System)이다.

![dbms](https://user-images.githubusercontent.com/42559714/44625449-df0f6b00-a944-11e8-94dd-3e45bcbf0f9d.PNG)

#### JDBC
JAVA 프로그램에서 SQL문을 실행하여 데이터를 관리하기 위한 JAVA API이다.
JDBC의 특징은 다양한 데이터 베이스에 대해서 별도의 프로그램을 만들 필요 없이, 해당 데이터 베이스의 JDBC를 이용하면 하나의 프로그램으로 데이터 베이스를 관리 할 수 있다.

#### 데이터 베이스 연결 순서

![12](https://user-images.githubusercontent.com/42559714/44636745-5e09af80-a9e8-11e8-90a3-3ee5d97651ad.PNG)

#### Statement 객체

![13](https://user-images.githubusercontent.com/42559714/44636863-e4be8c80-a9e8-11e8-9ad2-5873675f9de2.PNG)

![14](https://user-images.githubusercontent.com/42559714/44636912-2a7b5500-a9e9-11e8-9023-d03afba74de4.PNG)

### 커넥션 풀
**커넥션 풀(DataBase Connection Pool; DBCP)**<br />
클라이언트에서 다수의 요청이 발생하면 데이터베이스에서 커넥션 객체를 만드느라 서버에 부하가 생기게 된다. 이러한 문제를 해결하기 위해서 커넥션 풀은 미리 커넥션 객체를 만들어 놓고 요청이 들어오면 만들어 놓은 객체를 사용하여 부하를 줄인다.

![17](https://user-images.githubusercontent.com/42559714/44637803-4b927480-a9ee-11e8-8244-1944d96c5184.PNG)

### DAO
**DAO : Data Access Object**<br />
데이터 베이스에 접속해서 데이터 추가, 삭제, 수정 등의 작업을 하는 클래스이다.
일반적인 JSP 혹은 Servlet 페이지내에 위의 로직을 함께 기술할 수도 있지만, 유지보수 및 코드의 모듈화를 위해 별도의 DAO클래스르 만들어 사용한다.

### DTO
**DTO : Data Transfer Object**<br />
DAO클래스를 이용하여 데이터 베이스에서 데이터를 관리할 때 데이터를 일반적인 변수에 할당하여 작업할 수도 있지만, 너무 뒤섞여 난잡해질 수 있으므로 해당 데이터의 클래스를 만들어 사용한다.

![15](https://user-images.githubusercontent.com/42559714/44637428-04a37f80-a9ec-11e8-9921-c4b84feeef75.PNG)

### PreparedStatement
SQL문을 실행하기 위한 Statement객체는 중복코드가 많아지는 단점이 있다. 이러한 단점을 보완하기위해 PreparedStatement를 사용한다.

![16](https://user-images.githubusercontent.com/42559714/44637669-7f20cf00-a9ed-11e8-986a-75957028db10.PNG)

### 파일 업로드

### EL

### JSTL

### FrontContoller, Command 패턴

### Forwarding

