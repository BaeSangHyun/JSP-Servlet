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

## 웹프로그래밍이란
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

## Java Web
JAVA플랫폼(J2SE, J2EE, J2ME)중에서 J2EE를 이용한 웹프로그래밍
![web](https://user-images.githubusercontent.com/42559714/44499590-83807b80-a6bf-11e8-8ee9-933083dd6405.PNG)

## Servlet

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

### doGet(), dopost()



### Context Path

### Servlet 작동순서

### Servlet LifeCycle

### Servlet 선,후처리

### Servlet Parameter

### Encoding

### Servlet 초기화 파라미터 : ServletConfig

### 데이터 공유 : Servlet Context

### 웹어플리케이션 감시 : ServletContextListener


## JSP

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

### JSP 내부 객체
개발자가 객체를 생성하지 않고 바로 사용할 수 있는 객체.<br />
JSP에서 제공되는 내부객체는 JSP컨테이너에 의해 Servlet으로 변화될 때 자동으로 객체가 생성된다.

#### 내부 객체 종류
- 입출력 객체 : request, response, out
- 서블릿 객체 : page, config
- 세션 객체 : session
- 예외 객체 : exception
