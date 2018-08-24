# JSP-Servlet

## Content
- [웹프로그래밍이란](#웹프로그래밍이란)
- [Java Web](#java-web)
- [Servlet](#servlet)
    - [Servlet Mapping](#servlet-mapping)
        - [Servlet Mapping 방법](#servlet-mapping-방법)
    - [doGet(), doPost()](#doget-dopost)
    - [Context Path](#context-path)
- [JSP](#jsp)
    - [JSP 태그종류](#jsp-태그종류)
    - [JSP 동작원리](#jsp-동작원리)
    - [JSP 내부 객체](#jsp-내부-객체)
        - [내부 객체 종류](#내부-객체-종류)
    - [문법](#문법)
        - [Script](#script)
        - [지시자](#지시자)
        - [주석](#주석)
    - [request 객체](#request-객체)

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

### Servlet 작동순서

### Servlet LifeCycle

### Servlet 선,후처리

### Servlet Parameter

### Encoding

### Servlet 초기화 파라미터 : ServletConfig

### 데이터 공유 : Servlet Context

### 웹어플리케이션 감시 : ServletContextListener


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

### request 객체
`request` : 웹브라우저를 통해 서버에 어떤 정보를 요청하는 것

#### request객체 관련 메소드
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

### response 객체
`reponse` : 웹브라우저의 요청에 응답하는 것

#### response객체 관련 메소드
- `getCharacterEncoding()` : 응답할 때 문자의 인코딩 형태를 구한다.
- `addCookie(Cookie)` : 쿠키를 지정 한다.
- `sendRedirect(URL)` : 지정한 URL로 이동한다.


### Action 태그
JSP페이지 내에서 어떤 동작을 하도록 지시하는 태그.

- `foward` : 현재의 페이지에서 다른 특정페이지로 전환할 때 사용.<br />
`<jsp:forward page="*.jsp"/>`


