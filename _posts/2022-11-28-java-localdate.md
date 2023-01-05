---
layout: post
title: Java LocalDate (특정 시간 지났는 지, 특정 Format의 String을 LocalDate로)
categories: 
  - java
description: >
  
sitemap: true
---
Java LocalDate (특정 시간 지났는 지, 특정 Format의 String을 LocalDate로)

<br>
-   2시간이 지났는 지 확인

```java
import java.time.temporal.ChronoUnit;
import java.time.LocalDateTime;

// 2시간이 지난 과목 add
if (ChronoUnit.HOURS.between(subject.getUpdateTime(), LocalDateTime.now()) > 2) {
    updateSubjectList.add(subject);
}

// 마감 3일 이내의 컨텐츠만 가져오기
if(ChronoUnit.DAYS.between(LocalDate.now(), subjectContents.getEndDate()) > 3){
    continue;
}

// 3 출력
LocalDate localDate = LocalDate.now().minusDays(3);
System.out.println(ChronoUnit.DAYS.between(localDate, LocalDate.now()));

// 2 출력
LocalDateTime localDateTime = LocalDateTime.now().minusHours(2);
System.out.println(ChronoUnit.HOURS.between(localDateTime, LocalDateTime.now()));
```

<br>

----------
<br>

-   특정 Format의 String을 LocalDate(Time)으로 변환

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy M월 d일 m:s");
LocalDate date = LocalDate.parse(notice.getDate(), formatter);
```