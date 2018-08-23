# JSP-Servlet

## 1-1. 웹프로그래밍이란
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

## 1-2 Java웹
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
