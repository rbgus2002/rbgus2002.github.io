---
layout: post
title: Java 비동기처리
categories: 
  - java
description: >
  
sitemap: true
---

Java 비동기처리
# 왜 알아보았는가?

운영체제 수업 들으면서 교수님이 면접 때 많이 물어보는 3개가 다음과 같다고 함.

1. 비동기 처리
2. 인공지능
3. 메타버스

방학을 이용해서 Java 비동기 처리에 대해 공부해보려고 한다. (빠른 시일 내로 리눅스&스프링도 비동기처리 해볼 것) 비동기처리를 공부하기에 앞서, 시험 끝나고 종강하니까 하고싶은 공부할 수 있어서 너무 행복하다. ㅋ.ㅋ

또한, 크롤링을 통한 **LMS 연동 학업관리서비스** 프로젝트를 진행하면서 성능 문제의 이슈 때문에 비동기 처리의 절실함을 느꼈다. 단지 막연하게 순서가 보장되지 않아도 되기 때문에 비동기 처리를 이용하면 되지 않을까? 했지만 개념적으로 잘 이해하고 있다면 추후에 비슷한 이슈가 발생했을 때 빠르게 정답의 길로 나아갈 수 있을 것이다.

---

# 개요
Synchronous는 “sync”라고 불리며, 마찬가지로 Asynchronous는 “async”라 불린다. 프로그래밍 설계 관점에서 동기와 비동기의 개념을 잘 이해하는 것은 API를 설계하는 데 큰 도움이 된다. 특히 evented-based 설계와 오랜 시간이 소요되는 작업을 처리하는 데 유용하다.  
[https://www.mendix.com/blog/asynchronous-vs-synchronous-programming/](https://www.mendix.com/blog/asynchronous-vs-synchronous-programming/)

---

# 개념

### Synchronous : 동기

- 현재 작업중인 요청을 끝낸 뒤에 다음 요청을 수행할 수 있음
- A작업이 시작되면, 끝날 때까지 다음 작업인 B작업은 대기함.
- 요청을 하면 시간이 얼마가 걸리던지 요청한 자리에서 결과가 주어져야 함
- 작업 간에 dependency가 있는 경우 동기 방식으로 로직 만들어야 함
- single-thread model

장점

→ 설계가 매우 간단

단점

→ 작업중인 요청에 대해 결과가 주어질 때까지 아무것도 못하고 대기해야 함

### Asynchronous : 비동기

- 현재 작업중인 요청과 상관없이 동시에 여러 작업을 실행할 수 있음.
- 작업을 병렬적으로 실행
- **multi-thread model**
- non-blocking
- 비동기 방식으로 로직을 만들려면 작업 간에 dependency가 없어야 함 : independent
- 

장점

→ 동시에 작업이 가능하므로 response를 받기까지의 지연되는 시간을 감소시킴

단점

→ 설계가 다소 복잡

→ 순서 보장 X
  
![async1](https://user-images.githubusercontent.com/62997391/209843312-5a0ebc51-382d-459e-b5be-f9d3dc017807.png)  

![async2](https://user-images.githubusercontent.com/62997391/209843344-cac8668b-18d2-4823-abf2-25aba2bcc7b0.png)

---

# Multi-Threading in JAVA

자바에서 Thread를 만들기 위해 다음 2가지 작업을 해야 한다.

1. Thread 코드 작성
2. JVM에게 Thread를 생성하고 Thread 코드를 실행하도록 요청

Thread 코드를 작성하는 2가지 방법

- Thread Class 사용
- Runnable Interface 사용

### Thread Class를 통한 Thread 코드 작성

- java.lang.Thread
- Thread Class 다양한 메소드 참고 ([https://docs.oracle.com/javase/7/docs/api/java/lang/Thread.html](https://docs.oracle.com/javase/7/docs/api/java/lang/Thread.html))

1.. **Thread Class 상속**

  ```java
  public class ThreadExample extends Thread{

  }
  ```

2.. **run() 오버라이딩**

run() 메소드 안에 작성된 코드를 Thread 코드라고 부른다. run() 안에 작성된 코드를 스레드가 실행하기 때문에 run()안에 코드를 작성한다.

```java
public class ThreadExample extends Thread{
    @Override
    public void run() {
    }
}
```

```java
public class ThreadExample extends Thread{
    int i;

    public ThreadExample(int i) {
        this.i = i;
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread() + " : " + this.i);

        // 1초 대기
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}
```

3.. **Thread 객체 생성 및 start()**

Thread가 생명력을 가지고 실행을 시작하도록 start() 호출 → Thread 동작

```java
public class ThreadExample extends Thread{
    int i;

    public ThreadExample(int i) {
        this.i = i;
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread() + " : " + this.i);

        // 1초 대기
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}

class ThreadTest{
    public static void main(String[] args) {
        for(int i = 0 ; i < 10; i++){
            Thread threadExample = new ThreadExample(i);
            threadExample.start();
        }
        System.out.println("main thread end");
    }
}
```

4.. **결과**

Thread가 모두 수행되기 전에, 메인 메소드가 먼저 종료됨

```
main thread end
Thread[Thread-0,5,main] : 0
Thread[Thread-6,5,main] : 6
Thread[Thread-9,5,main] : 9
Thread[Thread-2,5,main] : 2
Thread[Thread-1,5,main] : 1
Thread[Thread-8,5,main] : 8
Thread[Thread-4,5,main] : 4
Thread[Thread-5,5,main] : 5
Thread[Thread-7,5,main] : 7
Thread[Thread-3,5,main] : 3
```

5.. **join()**

- fork()를 통해 자식 프로세스를 생성하고 wait()을 통해 자식 프로세스가 종료될 때까지 기다리는 것과 같음
- join()을 통해 각각 생성된 Thread가 종료될 때까지 main 메소드를 기다리게 함
- join()을 어디에 넣느냐에 따라 결과가 달라지니 직접 실습해보길 추천

```java
import java.util.ArrayList;
import java.util.List;

public class ThreadExample extends Thread{
    int i;

    public ThreadExample(int i) {
        this.i = i;
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread() + " : " + this.i);

        // 1초 대기
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}

class ThreadTest{
    public static void main(String[] args) throws InterruptedException {
        List<Thread> threadList = new ArrayList<>();
        for(int i = 0 ; i < 10; i++){
            Thread threadExample = new ThreadExample(i);
            threadExample.start();
            threadList.add(threadExample);
        }

        // 쓰레드 일단 모두 생성시켜놓고 join()을 통해 대기
        for(Thread thread : threadList){
            thread.join();
        }

        System.out.println("main thread end");
    }
}
```

6.. **결과**

```
Thread[Thread-5,5,main] : 5
Thread[Thread-2,5,main] : 2
Thread[Thread-8,5,main] : 8
Thread[Thread-9,5,main] : 9
Thread[Thread-7,5,main] : 7
Thread[Thread-0,5,main] : 0
Thread[Thread-4,5,main] : 4
Thread[Thread-1,5,main] : 1
Thread[Thread-3,5,main] : 3
Thread[Thread-6,5,main] : 6
main thread end
```

--- 

### Runnable Class를 통한 Thread 코드 작성
- Thread Class보다 더 빈번하게 사용됨
- java.lang.Runnable
- 추상 메소드 run() 하나만 가지고 있음

1.. **Runnable interface 구현**

```java
public class RunnableExample implements Runnable{
}
```   
  
2.. **run() 오버라이딩**

```java
public class RunnableExample implements Runnable{
    @Override
    public void run() {
        
    }
}
```

```java
public class RunnableExample implements Runnable{
    int i;

    public RunnableExample(int i) {
        this.i = i;
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread() + " : " + i);
        // 1초 대기
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}
```

3.. **Thread 객체 생성 및 start()**

```java
public class RunnableExample implements Runnable{
    int i;

    public RunnableExample(int i) {
        this.i = i;
    }

    @Override
    public void run() {
        System.out.println(Thread.currentThread() + " : " + i);
        // 1초 대기
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}

class RunnableTest{
    public static void main(String[] args) {
        for(int i = 0 ; i < 10; i++){
            Thread thread = new Thread(new RunnableExample(i));
            thread.start();
        }
    }
}
```

4.. **결과**

```
Thread[Thread-7,5,main] : 7
Thread[Thread-3,5,main] : 3
Thread[Thread-4,5,main] : 4
Thread[Thread-9,5,main] : 9
Thread[Thread-8,5,main] : 8
Thread[Thread-2,5,main] : 2
Thread[Thread-1,5,main] : 1
Thread[Thread-5,5,main] : 5
Thread[Thread-6,5,main] : 6
Thread[Thread-0,5,main] : 0
```

---

### 참고

[https://velog.io/@daybreak/동기-비동기-처리](https://velog.io/@daybreak/%EB%8F%99%EA%B8%B0-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%B2%98%EB%A6%AC)

[https://www.mendix.com/blog/asynchronous-vs-synchronous-programming/](https://www.mendix.com/blog/asynchronous-vs-synchronous-programming/)

[https://wikidocs.net/230](https://wikidocs.net/230)

[https://codechacha.com/ko/java-thread-join/](https://codechacha.com/ko/java-thread-join/)