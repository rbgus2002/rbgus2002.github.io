---
layout: post
title: Java 셀레니움 메소드 정리
categories: 
  - java
description: >
  
sitemap: true
---
셀레니움 메소드 정리 (Java)


# 세팅

**경로설정**

[직접 설정]
```java
public static String WEB_DRIVER_ID = "webdriver.chrome.driver";
public static String WEB_DRIVER_PATH = "/Users/choegyuhyeon/Downloads/chromedriver";

System.setProperty(WEB_DRIVER_ID, WEB_DRIVER_PATH);
```

[자동 설정]

**WebDriverManager**를 통한 드라이버 다운로드&경로 설정 자동화

```java
// bulid.gradle

implementation "io.github.bonigarcia:webdrivermanager:5.0.3"
```
```java
WebDriverManager.chromedriver().setup();
```
<br><br>

**옵션설정**


```java
ChromeOptions options = new ChromeOptions();

options.add_argument('headless') // **headless모드 브라우저가 뜨지 않고 실행됩니다**
options.add_argument('--window-size= x, y') // 실행되는 브라우저 크기를 지정할 수 있습니다.
options.add_argument('--start-maximized') // 브라우저가 최대화된 상태로 실행됩니다.
options.add_argument('--start-fullscreen') // 브라우저가 풀스크린 모드(F11)로 실행됩니다
options.add_argument('--blink-settings=imagesEnabled=false') **// 브라우저에서 이미지 로딩을 하지 않습니다.**
options.add_argument('--mute-audio') // 브라우저에 음소거 옵션을 적용합니다.
options.add_argument('incognito') // 시크릿 모드의 브라우저가 실행됩니다.

```
<br>

**드라이버 객체 생성**
```java
WebDriver driver = new ChromeDriver(options);
```
<br>

**브라우저 닫기**
```java
driver.close();
```
<br>

**모든 브라우저 닫기**
```java
driver.quit()
```
<br>

--- 

# 여러 기능

**웹페이지 이동**
```java
driver.get(url);
```

**프레임 이동**
```java
driver.switchTo().frame("tool_content");
```

**웹페이지 새로고침**
```java
driver.navigate().refresh();
```

**Element 찾기**
```java
element = driver.findElement(By.id("userid"));
element = driver.findElement(By.className("userid"));
element = driver.findElement(By.xpath("userid"));
element = driver.findElement(By.name("userid"));
element = driver.findElement(By.tagName("userid"));
```

**Element 클릭**
```java
element.click();
```

**텍스트 입력**
```java
driver.findElement(By.id("userid")).sendKeys("20182662");
```

**Explicit waits**
```java
WebElement firstResult = new WebDriverWait(driver, Duration.ofSeconds(10))
	.until(ExpectedConditions.elementToBeClickable(By.xpath("//a/h3")));

alertIsPresent() // 알림이 있는지 확인한다.
elementSelectionStateToBe() // 지정된 요소가 선택되었는지 확인한다.
**elementToBeClickable() // 요소가 표시되고 클릭할 수 있는지 확인한다.**
elementToBeSelected() // 요소가 선택될 수 있는지 확인한다.
frameToBeAvaliableAndSwitchToIt()
invisibilityOfTheElementLocated() // 페이지의 DOM에 요소가 보이지 않거나 존재하지 않는지 확인한다.
invisibilityOfElementWithText()
presenceOfAllElementsLocatedBy() // 페이지에 적어도 하나의 요소가 있는지 확인한다.
presenceOfElementLocated() // 페이지의 DOM에 요소가 있는지 확인한다.
textToBePresentInElement() // 주어진 텍스트가 지정된 요소에 있는지 확인한다.
textToBePresentInElementLocated()
textToBePresentInElementValue() // 주어진 텍스트가 지정된 요소의 로케이터에 있는지 확인한다.
titleIs() // 페이지의 title이 일치하면 True, 그렇지 않으면 False를 반환한다.
titleContains() // 페이지의 title에 대소문자를 구분하여 해당 문자열이 포함되어 있는지 확인한다. 포함되면 True, 그렇지 않으면 False를 반환한다.
visibilityOf() // 페이지의 DOM에 있는 요소가 보이는지 확인한다.
visibilityOfAllElements()
visibilityOfAllElementsLocatedBy()
visibilityOfElementLocated() // 요소가 페이지의 DOM에 있고 볼 수 있는 상태인지 확인한다. 볼 수 있다는 상태는 요소가 표시될 뿐만 아니라 높이와 너비가 0보다 커야 한다.
```