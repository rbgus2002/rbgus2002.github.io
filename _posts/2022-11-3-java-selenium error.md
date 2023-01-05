---
layout: post
title: Java Selenium Errors
categories: 
  - java
description: >
  
sitemap: true
---
Java Selenium Errors

## Error: “chromedriver” cannot be opened because the developer cannot be verified. Unable to launch the chrome browser

-   방법 1 >> Terminal에서 명령어 실행

```bash
# chromedriver 존재하는 디렉토리 이동 후
xattr -d com.apple.quarantine chromedriver;

```

-   방법 2 >> 환경설정 변경

1. First of all Open **System Preferences**.
2. Then Select **Security & Privacy**.
3. Under the General tab you are able to see like below Image.
4. Just click on **Open Anyway.**
5. Then You will see just like second image given below.
6. Just click on **Open**.
7. Now you can run selenium without any error.
<br><br>

---
## org.openqa.selenium.SessionNotCreatedException

![](https://blog.kakaocdn.net/dn/ByioD/btrQjmstStK/cdoyaUcj3Pks7a1BV7qcJK/img.png)

-   크롬 다운그레이드 해서 크롬 드라이버랑 버전도 정확히 맞춰보고 했는데 계속 에러떴음
-   [solved] 셀레니움 버전 3.4.0 이상 설치 시 해결됨
<br><br>

---

## not found web element

> 분명 알맞은 web element 이름으로 접근했는데 해당 이름을 Selenium이 찾지 못했다....... (3시간 삽질) => 멍청이

-   HTML 안에는 서브 HTML이 존재할 수 있음.
-   driver.get("~~~")을 통해 웹사이트 접속 시 가장 바깥 HTML에만 접근 가능
-   따라서 가장 바깥 HTML에서 서브 HTML에 존재하는 web element 접근 시도하면 NotFoundException Error 발생

결론 : 찾고자 하는 web element가 Sub HTML에 있으면 그 쪽으로 들어가자!