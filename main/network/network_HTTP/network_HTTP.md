# HTTP

생성 날짜: 2023/12/06 21:58

<aside>
💡 HTTP는 애플리케이션 계층으로 웹 서비스 통신에 사용됨

</aside>

## Section 2.5.1 HTTP/1.0
<hr>

HTTP/1.0은 기본적으로 한 연결당 하나의 요청을 처리하도록 설계되었기 때문에 서버로부터 파일을 가져올때마다 TCP-3 HandShake를 계속해서 열어줘야하기 때문에 RTT가 증가하는 단점이 존재

![image](https://github.com/cJinu/CS/assets/94429120/3be591b0-dc13-436f-a065-64efa965d054)

TCP 통신을 위한 네트워크 연결은 3-way handshake 라는 방식으로 연결됩니다. 서로의 통신을 위한 포트를 확인하고 연결하기 위하여 3번의 요청/응답 후에 연결이 되는 것을 말합니다. (위 이미지처럼) 이 과정에서 가장 많은 시간이 소요되어 UDP 방식보다 속도가 느려지는 주요 원인으로 지목됩니다.

RTT가 증가하니 서버에 부담이 많이 가고 응답 시간도 길어졌다

이를 해결하기 위한 기법은 다음과 같다.

- **이미지 스플리팅**
    - 웹페이지를 구성하는 다양한 이미지 파일의 요청 횟수를 줄이기 위해, 이미지들을 하나의 큰 이미지로 만든 다음 CSS에서 해당 이미지의 좌표 값을 지정해 표시하는 방법입니다.
- **코드 압축**
    - 코드를 압축해서 개행 문자, 빈칸을 없애 코드의 크기를 최소화하는 방법입니다.

```java
public class BOJ_9095_1_2_3_더하기 {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int T = Integer.parseInt(br.readLine());
        int[] dp = new int[12];
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 4;
        for(int i = 4; i <= 11; i++) dp[i] = dp[i-1] + dp[i-2] + dp[i-3];

        for(int i = 0; i < T; i++){
            int index = Integer.parseInt(br.readLine());
            System.out.println(dp[index]);
        }
    }
}
```

```java
public class BOJ_9095_1_2_3_더하기 {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine()); int[] dp = new int[12]; dp[1] = 1;dp[2] = 2; dp[3] = 4;
				for(int i = 4; i <= 11; i++) dp[i] = dp[i-1] + dp[i-2] + dp[i-3];
        for(int i = 0; i < T; i++){int index = Integer.parseInt(br.readLine());System.out.println(dp[index]);}
    }
}
```

- **이미지 Base64 인코딩 (Data URI Scheme)**
    - 이미지 파일을 64진법으로 이루어진 문자열로 인코딩하는 방법입니다.
    - 하지만 Base64 문자열로 변환할 경우 37% 정도 크기가 더 커지는 단점이 있습니다.
    - 자세한 설명은 영상을 보라더니 영상이 없네요…
    

> RTT
패킷이 목적지에 도달하고 나서 다시 출발지로 돌아오기까지 걸리는 시간
> 

## Section 2.5.2 HTTP/1.1

---

<aside>
💡 매번 TCP 연결을 하는것이 아닌, keep-alive라는 옵션을 통해 한번의 연결로 여러개의 파일을 송수신이 가능해짐
1.0에서도 존재했지만 표준화가 되지 않았고, 1.1에서 표준화

</aside>

![image](https://github.com/cJinu/CS/assets/94429120/aef2ebc8-4467-4641-a9a2-827eb2ec17f2)

한번의 TCP 통신을 통해 여러개의 Request와 Response가 왔다갔다하는 모습

하지만 문서 안에 포함된 리소스들이 많을수록 대기시간이 오래걸린다.

### HOL Blocking

네트워크에서 같은 큐에 있는 패킷이 이전에 있던 리소스에 의해 지연될 때 발생되는 성능 저하 이슈

![image](https://github.com/cJinu/CS/assets/94429120/84c3ecd1-1a07-4c05-b481-8c360ab7c1b8)

순차적으로 받아야하기 때문에 image.jpg가 다 다운이 될 때 까지 그 뒤의 리소스는 대기를 해야한다.

HTTP 1.1의 헤더 구조는 아래와 같다.

![image](https://github.com/cJinu/CS/assets/94429120/94b4db80-22c5-49e8-bee3-fc358d22f34a)

눈에 익숙한 cookie, date, cache 등이 존재하고 그를 제외하고도 다양한 메타데이터들이 존재

이는 압축이 되지 않아 무겁다.

## Section 2.5.3 HTTP/2

---

<aside>
💡 HTTP/2는 HTTP/1.x보다 지연시간을 줄이고 응답시간을 더 빠르게할 수 있으며 
멀티플렉싱, 헤더압축, 서버 푸쉬, 요청의 우선순위 처리를 지원하는 프로토콜

</aside>

### 멀티플렉싱

---

여러개의 스트림을 사용해서 송수신

특정 스트림의 패킷은 손실되어도 나머지 패킷은 정상적으로 작동가능

![image](https://github.com/cJinu/CS/assets/94429120/4b6c0b7d-21a6-4e5c-8dc4-360646db9684)

![image](https://github.com/cJinu/CS/assets/94429120/411da0d2-3988-4a1f-a897-1db4543a1695)

Index.html를 로딩한다고 하면 그 안에 있는 이미지, css, js등의 여러 파일을 쪼개서 전달한 후 
전달이 완료되면 서로 조립하여 데이터를 주고받는 방식

### 헤더 압축

---

HTTP/1.x 버전에서는 크기가 큰 헤더라는 문제가 존재했는데 이를 허프만 코딩 압축 알고리즘을 이용하는 HPACK 압축 형식으로 해결

<aside>
💡 허프만 코딩이란?
코드를 문자 단위로 쪼개서 빈도수가 높은 문자는 적은 비트 수를 사용하고 빈도수가 낮은 문자는 비트 수를 많이 사용해서 표현하여 용량을 최대한 압축하는 방식

</aside>

### 서버푸시

---

클라이언트가 INDEX.html을 요청하고 그 안에 있는 css, js는 index.html을 받고난 후에 클라이언트가 다시 요청을 보내는데 HTTP/2에서는 클라이언트의 요청없이 바로 해당 파일을 푸시 가능하다.

![image](https://github.com/cJinu/CS/assets/94429120/eacc147a-a614-4ffd-bdca-f14e61199ee5)

## Section 2.5.4 HTTPS

---

HTTPS는 애플리케이션 계층과 전송 계층 사이에 있는 신뢰 계층인 SSL/TLS 계층을 넣은 신뢰할 수 있는 HTTP, 즉 암호화 된 통신을 의미함

### SSL/TLS

---

SSL(Secure Socket Layer), TLS(Transport Layer Security Protocol)을 합친 말로 전송 계층에서 보안을 제공하는 프로토콜

클라이언트와 서버간의 통신을 제3자가 도청 또는 변조를 하지 못하게 함

### 보안 세션

---

클라이언트와 서버가 통신을 처음으로 시작할 때 TLS 핸드쉐이크를 딱 한번 진행한다.

![image](https://github.com/cJinu/CS/assets/94429120/baaa1c2a-6876-4c85-b766-9ba20cd8ad9e)

서버와 클라이언트가 키를 공유하고, 인증, 인증확인 등이 진행된다.

클라이언트가 사이퍼 슈트를 서버에게 전달하면 서버는 클라이언트에게 받은 사이퍼 슈트를 통해 암호화가 알고리즘 리스트를 제공할 수 있는지 확인 후 제공이 가능하다면 인증 메커니즘이 시작되고 암호화된 데이터의 송수신이 시작된다.

<aside>
💡 사이퍼슈트란?
프로토콜, AEAD 사이퍼 모드, 해싱 알고리즘이 나열된 규약을 의미

AEAD 사이퍼 모드란?
Authenticated Encryption With Associated Data의 약자이며 데이터 암호화 알고리즘을 의미

</aside>

### 암호화 알고리즘

---

암호화 알고리즘의 대표적인 예시는 두개가 있다.

1. 암호키를 교환하는 디피-헬만 알고리즘
2. 데이터를 해싱하는 SHA-256 알고리즘

### 디피-헬만 키 교환 알고리즘

---

$$
y=g^xmod p
$$

학교에서 한번쯤은 공부해봤을 디피-헬만 식

g, x, p 를 안다면 구하기는 쉽지만 x를 구하기는 쉽지 않다는 원리

![image](https://github.com/cJinu/CS/assets/94429120/a00326b7-be2e-45c8-92f7-0c41cd1067e3)

위의 그림을 색깔에 주목하면 g는 노란색 즉 공개키

각각의 비밀키 x는 서로 다르기 때문에 주황색, 청록색

이제 노란색과 주황색, 노란색과 청록색을 섞어서 연노랑, 연파랑이 나왔다.

연노랑과 연파랑을 서로 교환한 후 각자의 개인키인 주황색과 청록색을 섞으면 같은 색깔이 나온다.

1. generator라고 불리는 공개키를 생성
2. 클라이언트와 서버는 각자의 개인키를 이용해 g^x mod p를 생성한다 (이때 p는 반드시 소수)
3. 클라이언트의 개인키를 C, 서버의 개인키를 S라고 할 때, 클라이언트는 서버에게 g^c mod p
서버는 클라이언트에게 g^S mod p 를 전송한다.
4. 마지막으로 각자의 개인키를 이용해서 g^CS mod p 를 만든다.
5. 이렇게 생성된 값을 대칭키로 사용한다.

### 디피헬만의 취약점

---

대칭키를 비밀스럽게 만들수있다는 장점이 있지만, 공격자가 중간에 데이터를 가로채서 
g^S mod p와 g^C mod p를 공격자의 개인키를 이용하여 g^A mod p로 클라이언트와 서버로 전송한다.

그렇게 되면 서로 g^AC mod p, g^AS mod p를 각각 대칭키로 가지고 있게 되고, 공격자는 

둘 다 가지고 있기 때문에 클라이언트, 서버, 공격자는 모두 같은 대칭키를 가지고 있게 되기 때문에 공격을 받을수있게 된다.

<aside>
💡 모듈러 연산을 소수로 하는 이유

</aside>

![image](https://github.com/cJinu/CS/assets/94429120/36d65dcf-33d6-41d0-a80e-6f28a2cd524d)

![image](https://github.com/cJinu/CS/assets/94429120/401bb847-d525-4856-81a3-ff2c861c35e5)

결과값을 보면 모듈러 연산을 했을 때 모든 값이 균일하게 나온것을 알 수 있다.

### 해싱 알고리즘

---

해싱 알고리즘이란 데이터를 추정하기 힘든 더 작고, 섞여 있는 조각으로 만드는 알고리즘

해싱 알고리즘의 대표적인 예시인 SHA-256은 결과값이 언제나 256비트인 알고리즘이다.

원본 데이터에 특정 문자열을 추가하는 등에 전처리 작업을 진행 후 해싱을 진행한다.

![image](https://github.com/cJinu/CS/assets/94429120/8dfec47b-07d6-47c5-9bc6-283f4ec7aee2)

1. 변환하고자 하는 데이터를 바이너리 형태로 변환한다.
2. 메시지의 마지막에 1비트를 추가한다.
3. 1 비트 뒤에 0으로 채워 나머지 공간을 채운다. (마지막 64비트를 제외한 448비트까지 채움)
4. 마지막 64비트는 원래 문자열의 길이를 Big Endian 정수로 나타낸다
5. 이렇게 나온 512비트를 다시 32비트로 자른다
6. 압축 함수를 64번 반복한다.
7. 각 블락별로 해시 값을 구하여서 이전 블록이 다음 블록의 입력값이 되어 최종적으로 256비트의 해시값이 생성된다.

만일 무한대의 시간과 자원이 있다면 해킹할 수 있지만, 현재까진 아무도 해내지 못했다고 합니다.

### SEO에도 도움이 되는 HTTPS

---

SEO(Search Engine Optimization)는 검색엔진 최적화를 뜻하며 캐노니컬 설정, 메타 설정, 페이지 속도개선, 사이트맵 관리등의 방법이 있다.

- 사이트맵 관리
    - sitemap.xml을 관리
    - *사이트맵*은 사이트에 있는 페이지, 동영상 및 기타 파일과 그 관계에 관한 정보를 제공하는 파일입니다.
    - Google과 같은 검색엔진은 이 파일을 읽고 사이트를 더 효율적으로 크롤링합니다.
    - 사이트맵은 내가 사이트에서 중요하다고 생각하는 페이지와 파일을 Google에 알리고 중요한 관련 정보를 제공
    - 페이지가 마지막으로 업데이트된 시간, 페이지의 대체 언어 버전

- 캐노니컬 설정
    - 검색엔진이 어떤 URL이 표준 URL인지 판단할 수 있게하는 태그
    - 만일 여러개의 URL이 결국엔 하나의 URL로 통하게 된다면 어떤 URL이 메인인지 판단할 수 있게 하는 태그
    - 캐노니컬을 사용하면 해당 페이지의 URL을 통해서 해당 페이지를 URL로 사용하는 하위 페이지의 수를 파악할 수 있고, 검색엔진의 자원도 절약이 가능하다.

![image](https://github.com/cJinu/CS/assets/94429120/e02d8807-2396-441a-b245-3175ad6ecb06)

![image](https://github.com/cJinu/CS/assets/94429120/5456020a-ff6e-46ba-8019-7835e085eabe)

canonical로 사용된 URL에 접근을 시도했는데 권한이 없어서 접근이 되지않는다… 구글…

이녀석들 뭔가를 숨기고 있다….

- 메타설정
    - 메타란 웹 컨텐츠로 화면에 표시되는것이 아닌 웹 페이지에 대한 정보를 제공하는 태그
    - 주로 검색엔진이 웹 페이지에 대한 추가적인 정보를 얻기 위해 메타 데이터를 사용
    - 페이지의 랭킹 또는 검색 결과를 나타내는데 사용
    - title과 description이 제일 중요하다고 함!
    

![image](https://github.com/cJinu/CS/assets/94429120/e0450fb9-d78c-404a-9bb4-aba8b82b33c9)

EnjoyTrip에 사용된 index.html의 메타

- 페이지 속도 개선
    - 이건 너무나도 당연하게 느린 페이지는 사용자가 이용하기를 꺼림
    

## Section 2.5.5 HTTP/3

---

- HTTP/3는 2와는 다르게 TCP 위에서 돌아가는것이 아닌 QUIC라는 계층에서 TCP가 아닌 UDP 기반으로 돌아감
- HTTP/2의 장점인 멀티플렉싱을 계승하여 초기 연결시 지연시간감소을 유지
- 

![image](https://github.com/cJinu/CS/assets/94429120/7690cf20-9fec-4df4-aba4-d86e105dca81)

HTTP/2와 HTTP/3의 차이점은..

1. QUIC라는 전송 계층 프로토콜 사용
2. TCP대신 UDP를 사용

### QUIC

---

- QUIC(Quick UDP Internet Connection)는 구글에서 개발하여 현재 구글 서비스의 약 절반정도는 QUIC로 처리되고 있다.
- 전세계로 연결되고 있는 네트워크의 특징 상 인스타그램, 유튜브 등등 다양한 해외기업 서비스를 사용하는데 기존 TCP는 지연이 발생할 수 밖에 없는 조건을 가지고 있다.
- 이론적으로 0-RTT 가능
- TCP보다 UDP가 헤더구조가 더 가볍기 때문에 더 빠르게 인터넷 연결을 하는 새로운 프로토콜

- QUIC HandShake 과정
    - 최초연결시
        1. client hello를 Server에 전송
        2. 소스 주소 토큰과 서버 인증서를 포함하여 Client에 전송
        3. Complete client hello를 server에 전송하면 quic HandShake 완료
    - 재연결 시
        1. 이전 연결의 캐시된 자격 증명을 사용해서 암호화된 요청을 즉시 서버로 요청
    - Client의 캐시 정보가 오래된 경우
        1. 최초연결의 행위를 반복

### HTTP/3의 문제점

---

1. QUIC는 패킷별로 암호화를 하기 때문에 멀티플렉싱을 사용하는 QUIC의 경우 더욱 많은 리소스를 사용할 우려가 있다
2. 기존 체계와의 호환이 아직 유연하지 않아서 이미 충분한 인프라를 구축한 기업의 경우 QUIC의 도입이 성능을 더 약화시킬수도 있다.
3. 기존 프로토콜보다 CPU의 사용량이 많음

<aside>
💡 TCP가 지연이 발생할 수 밖에 없는 이유

![image](https://github.com/cJinu/CS/assets/94429120/b4b63ba7-92ed-4013-ae6f-359d84da22c6)

TCP는 신뢰성을 보장하는 연결형 서비로스로 클라이언트와 서버가 연결 된 상태에서 데이터를 주고받는 프로토콜이다.

안정적, 순차적, 에러없이 데이터를 교환할 수 있다.

이를 3-way-handshake를 통해서 보장하는데 이 handShake 때문에 UDP보다 속도가 느릴수밖에 없는 구조

</aside>

<aside>
💡 TCP와 UDP의 차이
UDP는 비연결형 통신 프로토콜로 TCP와 다르게 데이터의 전송 순서, 수신 여부등이 없어서 TCP보다 신뢰성이 낮은 대신 속도가 빠르다.
연속성 있는 전송이 중요한 실시간 라이브, 게임등에 사용된다.

![image](https://github.com/cJinu/CS/assets/94429120/d726cbc7-24f0-4003-8a0f-352476208e32)

</aside>

### HTTP 버전별 차이

| HTTP/1.0 | HTTP/1.1 | HTTP/2.0 | HTTP/3.0 |
| --- | --- | --- | --- |
| 하나의 파일당 하나의 커넥션 | 하나의 커넥션 당 여러개의 파일  | 멀티플렉싱을 통해서 한번의 Request에 여러개의 파일 요청 가능 | QUIC를 통해서 더 가볍고 빠르게 통신 가능 |

리다이렉트 - 리다이렉트가 있다면 진행 없다면 그대로 해당 요청에 대한 과정이 진행

캐싱 - 캐싱이 가능한지 확인 후 캐싱이 가능하면 캐싱된 값을 반환하고 그렇지 않다면 그 다음 단계로 넘어간다 

DNS - 도메인 이름을 IP주소로 바꿔줌

DNS캐싱 

IP 라우팅

TCP 연결 구축

콘텐츠 다운로드

브라우저 렌더링