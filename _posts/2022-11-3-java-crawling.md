---
layout: post
title: Java 웹 크롤링 하기 (Selenium)
categories: 
  - java
description: >
  
sitemap: true
---
Java로 웹 크롤링 하기 (Selenium)

## 어떤 프레임 워크 쓰지?
---

Java로 웹 크롤링을 하기 위해서 선택할 수 있는 경우의 수는 보통 2가지이다.
- Jsoup
- Selenium
<br>

### Jsoup
-   static한 데이터 수집하는 경우에 주로 사용
-   빠르지만 브라우저가 아닌 HTTP Request를 사용해서 동적 데이터 수집하려면 해당 서버 인증키 요구 등 수집할 수 없는 경우가 존재한다. 따라서 동적인 데이터 가져오는 데는 비적합
### Selenium
-   dynamic한 데이터 수집하는 경우에 주로 사용
-   Jsoup에 비해 속도는 느리지만 HTTP request가 아닌 브라우저 드라이버 사용해서 동적 데이터 수집 가능

<br>

>**Static Data**  vs **Dynamic Data**

Static → 한 페이지에서 원하는 정보가 모두 드러남 <br>
Dynamic → 입력, 클릭, 로그인 등과 같이 페이지 이동이 있어야 보임

<br>
---
# Selenium

#### 1. Chrome 버전 확인
![image](https://user-images.githubusercontent.com/62997391/210830253-8e74de2e-2534-40d4-81bf-cafef884a203.png)

브라우저 열기 → 설정 → Help → About Google Chrome<br>
셀레니움을 사용하기 위해 크롬 브라우저 버전을 알 필요가 있다. 위 과정을 통해 크롬의 버전을 확인하자.<br><br>

####  2. Chrome WebDriver 다운로드
자신의 크롬 버전과 맞는 드라이버를 설치한다.
[https://chromedriver.chromium.org/downloads](https://chromedriver.chromium.org/downloads)  여기서 다운로드 하자.
만약 크롬 쓸 거 아니면 다른 브라우저의 드라이버 설치 gogo
<br>

#### 3. Selenium 설치
**Maven**

```bash
<!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java -->
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>3.4.0</version>
</dependency>
```

**Gradle**

```groovy
// <https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java>
compile group: 'org.seleniumhq.selenium', name: 'selenium-java', version: '3.4.0'
```
<br>

#### 4. 예제 코드 실행
```bash
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class Test {
    public static void main(String[] args) {
        System.setProperty("webdriver.chrome.driver", "<크롬 드라이버 경로>");

// 브라우저 실행
        WebDriver driver = new ChromeDriver();

// 구글 홈페이지로 이동
        driver.get("<http://www.google.com>");
    }
}
```