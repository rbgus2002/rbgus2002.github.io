---
layout: post
title: 스프링부트 Swagger 사용하기
categories: 
  - java
description: >
  
sitemap: true
---
스프링부트 Swagger 사용하기


## 왜 사용해야 하는가

BE와 FE는 협업을 위해 API 명세서 작성이 필수적이다. 명세서 작성은 다소 번거로운 작업이지만, Spring Boot에는 이러한 API 명세서를 쉽게 작성해줄 수 있는 기능을 제공한다.
지금까지 Notion을 활용해서 명세서를 작성했지만 앞으로는 Swagger를 적극 활용하려고 한다. 써보니 진짜 너무 편함..

## 장점

-   API가 수정이 되더라도 문서가 자동으로 업데이트 됨
-   간편하게 REST API를 문서화할 수 있음
-   문서화 뿐 아니라 빌드, 테스트 케이스도 작성 가능

## 라이브러리

보통 아래 두 개의 라이브러리를 사용함.

-   **springdoc**  vs springfox

![](https://blog.kakaocdn.net/dn/Nzom0/btrTQwkxERY/VqulIRRbtq8Zik1GTp9iIK/img.png)

**springdoc**를 통해 Project에 Swagger를 적용하자!

--- 

<br>

## Swagger 3.0

-   springdoc 공식문서 :  [https://springdoc.org/](https://springdoc.org/)

<br>

## 1. dependency 추가

```java
dependencies {
    implementation 'org.springdoc:springdoc-openapi-ui:1.6.9'
}
```

<br>

## 2. Config Class 생성

```java
// SwaggerConfig.java
package com.project.LMSSU.Config;

import io.swagger.v3.oas.annotations.OpenAPIDefinition;
import io.swagger.v3.oas.annotations.info.Info;
import lombok.RequiredArgsConstructor;
import org.springdoc.core.GroupedOpenApi;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@OpenAPIDefinition(
        info = @Info(title = "LMSSU API 명세서",
                description = "LMS 연동 학업관리 서비스 API 명세서",
                version = "v1"))
@RequiredArgsConstructor
@Configuration
public class SwaggerConfig {
}

```

<br>

## 3. application.properties 추가

path 지정을 통해 swagger 접속 → /api-docs

```gradle
# swaggerdoc
springdoc.version=v1.0.0
springdoc.packages-to-scan=com.project.LMSSU.Controller
springdoc.swagger-ui.path=/api-docs
springdoc.swagger-ui.tags-sorter=alpha
springdoc.swagger-ui.operations-sorter=alpha
springdoc.api-docs.groups.enabled=true
springdoc.cache.disabled=true
springdoc.default-consumes-media-type=application/json;charset=UTF-8
```

<br>

## 4. Swagger 접속

-   [http://localhost:8080/api-docs](http://localhost:8080/api-docs)

![](https://blog.kakaocdn.net/dn/vyRcr/btrTR8XcuQr/MCX9wg8u48e3UzaPPMWKWK/img.png)

<br>

## 5. 실제 컨트롤러에 적용

```java
@RestController
@RequiredArgsConstructor
@RequestMapping("/list")
@Tag(name = "SubjectList Controller", description = "과목 리스트 컨트롤러")
public class SubjectListController {
    private final SubjectListService subjectListService;

    @Operation(summary = "[과목 리스트] 특정 주차의 과목 리스트를 불러온다.", description = "크롤링이 필요한 과목은 크롤링 후에 과목 리스트를 불러온다.")
    @PostMapping()
    public SubjectListResponseDTO getSubjectInfoList(@RequestBody StudentLoginRequestDTO dto, @RequestParam Integer week) throws InterruptedException {
        System.out.println("!@#!@# getSubjectInfoList");
        return subjectListService.getLMSInfo(dto, week);
    }

    @Operation(summary = "[과목 리스트] To-Do-List 추가 API", description = "DB에 To-Do-List를 추가한다.")
    @PostMapping("/todo")
    public Map addToDo(@RequestBody ToDoRequestDTO dto) {
        System.out.println("!@#!@# addToDo");
        return subjectListService.addToDo(dto);
    }

    @Operation(summary = "[과목 리스트] To-Do-List 삭제 API", description = "입력받은 To-Do-List와 일치하는 정보가 있다면 삭제시킨다.(isUsed -> false)")
    @GetMapping("/todo/cancel")
    public Map cancelToDo(@RequestParam Long toDoId) {
        return subjectListService.deleteToDo(toDoId);
    }

    @Operation(summary = "[과목 리스트] To-Do-List 체크 API", description = "입력받은 To-Do-List와 일치하는 정보가 있다면 isDone -> true로 설정한다.")
    @GetMapping("/todo/check")
    public Map checkToDo(@RequestParam Long toDoId) {
        return subjectListService.checkToDo(toDoId);
    }

    @Operation(summary = "[과목 리스트] To-Do-List 체크 해제 API", description = "입력받은 To-Do-List와 일치하는 정보가 있다면 isDone -> false로 설정한다.")
    @GetMapping("/todo/check/cancel")
    public Map cancelCheckToDo(@RequestParam Long toDoId) {
        return subjectListService.deleteCheckToDo(toDoId);
    }
}
```

<br>

## 6. 적용 후 Swagger

![](https://blog.kakaocdn.net/dn/cciCIh/btrTRCRQRwg/f5AviJmKNBkUxBg72bjANK/img.png)

![](https://blog.kakaocdn.net/dn/lupzR/btrTPWqworb/4iJpEfI7akWgekfSpACAVK/img.png)

>Try it out을 통해 API 테스트 가능 Good Good

<br><br>

참고 사이트 :  [https://oingdaddy.tistory.com/272](https://oingdaddy.tistory.com/272)