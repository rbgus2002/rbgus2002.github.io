---
layout: post
title: 첫 공모전, 회고록
categories: 
  - retrospective
description: >
  [제5회 KB국민은행 소프트웨어 경진대회](https://www.kbsccoding.com/)
sitemap: true
---




# 첫 공모전, 회고록

----------

사실 첫 공모전은 아니다. 작년에 교내 공모전에 나간 경험은 있지만, 아무 것도 모르고 나갔을 때라 이번이 사실상 처음이라 하겠다.

대학교 동기 4명과 KBSC 공모전에 나갔다. 지금 생각해보니 이번에도 뭣 모르고 나갔다. 스프링이라고는 해본 적도 없는 우리였고 하이브리드 앱 만들겠다고 리액트를 공부했는데 알고보니 웹 만드는 프레임워크라더라. 그래서 중간에 안드로이드 개발로 계획을 바꿨다. 다시 생각해봐도 **총체적 난국**이다.

<br>

# 프로젝트를 진행하며

----------

우리 팀원 5명 모두 특별히 잘하는 거 없는 그런 사람들이다. 아니 오히려 할 줄 아는 게 없는 그런 사람들이 더 맞는 표현 같다. 내가 그나마 회사에서 인턴중이니 백엔드와 프론트 간의 협업 방식은 알고 있기에 내가 직접 프로젝트를 주도하며 30년 정도 부식된 톱니바퀴처럼 우리 팀이 굴러갔다.

<br>


## 1. 기획

거리가 멀음에도 불구하고 다같이 숭실대학교에 모여 머리를 맞대고 고민했다. 구체적으로 회의록도 적었으면 좋았으련만, 그 간의 노력하는 과정들이 기억에서 잊혀졌다..

KBSC 공모전의 주제는 다음과 같다.

>💡 국민과 함께 『세상을 바꾸는 소프트웨어』 - '**환경**'과 '**사회공헌**' 2가지 주제 중 1개를 택하여 지원

우리는 환경이라는 주제를 택했고 구체적으로 플로깅에 대해 프로젝트를 진행해보기로 했다. 기획 단계에서 최대한 추후에 수정하는 일이 없도록 자세히 기획했는데, 안드로이드 앱 내에서 카카오맵을 연동하고 플로깅을 할 수 있도록 도움을 주는 서비스를 개발하는 것이 목표였다.

-   서울 시 내의 쓰레기통 위치를 공공 데이터 API로 가져와 본인 주변 쓰레기통이 어디있는 지 지도 내에서 확인할 수 있는 기능
-   지도에서 플로깅 시작 버튼을 만들어서 걸음수 측정, 시간 측정 기능
-   플로깅이 끝난 뒤 인스타그램 스토리 공유 기능
-   위치 기반으로 동네 사람들과 플로깅을 할 수 있도록 앱 내에 커뮤니티 생성 (지역 선택). 당근 마켓 동네 생활 기능 처럼 만들고자 함.

<br>

## 2. 설계

**Work Flow**

[Whimsical work flow](https://whimsical.com/kb-esg-R7KRxom9XbMyQaqLitj317)


**ERD**
![Untitled](https://user-images.githubusercontent.com/62997391/210916306-e0105795-a037-4bba-9cd3-f0c18b94bed0.png)


**API 명세서**

백에서 API 만들면 노션에다가 정리 후 Postman으로 테스트 했다. (이 땐 Swagger를 몰랐었다. 지금은 Swagger 없으면 너무너무 불편하다 ㅠ)
![Untitled 1](https://user-images.githubusercontent.com/62997391/210916500-e11fcdfd-8272-4fd6-a76e-afa79301badd.png)

### UseCase

나의줍깅

![image](https://user-images.githubusercontent.com/62997391/210916673-829b0caa-c34a-4536-8391-e6778ed0ffd3.png)

랭킹

 ![image](https://user-images.githubusercontent.com/62997391/210916685-d333c920-054c-4213-83d6-97530e94a6a6.png)

로그인

![image](https://user-images.githubusercontent.com/62997391/210916692-e227e458-172c-42f5-8a88-b017a43e1972.png)

지도보깅

![image](https://user-images.githubusercontent.com/62997391/210916703-9e8eb8cc-a81a-4845-832f-9750d6ffaeb5.png)

포인트샵

![image](https://user-images.githubusercontent.com/62997391/210916714-2758a30b-54e6-4101-8590-946adcab0eec.png)

프로필

![image](https://user-images.githubusercontent.com/62997391/210916723-e4811391-5d27-4f96-9193-f137a6537ad2.png)

함께줍깅

![image](https://user-images.githubusercontent.com/62997391/210916735-44f9f673-0bbd-4c7f-a31a-4a0da8280b86.png)

<br>

## 3. 구현 기능
![image](https://user-images.githubusercontent.com/62997391/210917243-770c7b5d-a0f3-4746-ace8-4a64e42ece44.png)
![image](https://user-images.githubusercontent.com/62997391/210917258-d7f5665c-3db4-4c3c-acad-e6a49aeabcd7.png)
![image](https://user-images.githubusercontent.com/62997391/210917269-a5b0682c-7954-4a0b-abab-eb768f10611c.png)
![image](https://user-images.githubusercontent.com/62997391/210917283-0a3f4b51-4ff1-4a42-896b-ee821444b0a6.png)
![image](https://user-images.githubusercontent.com/62997391/210917298-6b19f7a1-9214-4f4a-ae7c-8a3cb962b537.png)
![image](https://user-images.githubusercontent.com/62997391/210917312-d6efa3cc-8581-4d1f-bd15-ed51f8adf49c.png)
![image](https://user-images.githubusercontent.com/62997391/210917336-3c2ec6b8-f815-4d11-b92e-272ee1a5d4e7.png)
![image](https://user-images.githubusercontent.com/62997391/210917347-faf8cc52-1709-49ef-88c9-c33d17fca6b4.png)
![image](https://user-images.githubusercontent.com/62997391/210917360-ac1d9242-0d4c-4b8b-bad9-096fe11dbd2f.png)
![image](https://user-images.githubusercontent.com/62997391/210917372-bc560d61-1e36-4688-ace5-781722a3b960.png)
![image](https://user-images.githubusercontent.com/62997391/210917386-ee12714d-84bc-4362-94ea-b4b338a08d7a.png)
![image](https://user-images.githubusercontent.com/62997391/210917399-2d01acbc-268b-4b2a-a99a-7b7819de4c9a.png)
![image](https://user-images.githubusercontent.com/62997391/210917405-2cfaa256-9731-4fea-a4cf-851b14a29d21.png)
![image](https://user-images.githubusercontent.com/62997391/210917416-67129ba7-4e06-420e-884d-90fa03386e71.png)
![image](https://user-images.githubusercontent.com/62997391/210917421-77c345cf-bbe6-466e-af15-a09d79841e2f.png)
![image](https://user-images.githubusercontent.com/62997391/210917434-5f1b312c-cbd6-4899-ae7d-967ef583bcaa.png)
![image](https://user-images.githubusercontent.com/62997391/210917451-4a0ed16d-b992-4685-92fb-30ec9a17fd1a.png)
![image](https://user-images.githubusercontent.com/62997391/210917459-34be5e16-5fae-4121-b0c9-8ab78e064272.png)
![image](https://user-images.githubusercontent.com/62997391/210917468-a8847ae8-7b6d-43eb-b3a6-285fd4d1e95c.png)
![image](https://user-images.githubusercontent.com/62997391/210917473-fce5c27c-2d65-4742-b13b-188b8c7d54bc.png)


<br>

### 4. 결과물

[실행 동영상](https://www.youtube.com/watch?v=pA0kIA1dKKI)

[추후 보고서 추가]()

<br>

# 너무 아쉬운데..

----------

솔직히 잘했다고 생각했다.

첫 시작은 오합지졸이었지만 무식하면 용감하다고 우리는 용감하게 척척 프로젝트를 진행해나갔었다. 회의를 통해 주제로 플로깅을 선정했고, 이는 시의성이 있고 점점 주목을 받는 분야기에 수요도 높아서 승산이 있다고 생각했다. 또 노션으로 협업도 잘이루어져 손발이 척척 맞는다고 생각했다. (이 때까지만 해도 Swagger의 존재를 몰랐다.. Swagger 최고)

하지만 결과는 예선 탈락이었다.. 약 2달간을 준비하며, 특히 제출 직전엔 이틀 밤을 새가며 유즈케이스도 그리고 보고서도 열심히 써서 더 아쉬었다.

사실 프로젝트가 끝난 시점으로 반년 뒤에 쓰는 회고록이라 기억이 잘 안났지만 더듬더듬해서 썼다. 선명하게 모든 장면이 기억이 나는 건 아니지만 아쉬웠던 그 감정만큼은 뚜렷하다.

예선탈락을 해서 아쉬웠던 것도 있지만, 탈락이라는 사실 자체로 실망하는 것이 아니라 우리의 어떤 점이 부족했고 부족한 점을 어떻게 채울 수 있을까 고민했다. 그래서 메일로 여쭤보았다. 혹시나 실례가 될까봐 최대한 조심조심.. 글을 적었다.
![image](https://user-images.githubusercontent.com/62997391/210917103-dbeb61a4-df49-4fba-b05a-460740fbc044.png)

이렇게 메일을 보냈는데 하루만에 답장이 왔다.
<br>
![image](https://user-images.githubusercontent.com/62997391/210917116-e568ef05-2989-45f7-8e37-a11ecf323699.png)

이러한 말씀을 들으니 다시 돌아보게 되었다. 정말 객관적으로 주제가 참신하고 좋았을까? 구현면에서 부족한 점이 많진 않았을까?  
피드백을 원했지만 아무래도 거기까진 무리였나보다. 담담히 결과를 받아들이기로 했다.  
패배의 쓴 맛을 본 것 같다. 아빠한테 말했더니 진짜 실패를 감내하려면 이런 사소한 패배도 겪어봐야 한다고 한다. 맞는 말이다. 근데 아빠는 정말 MBTI가 T인 거 같다ㅋㅋ; 참나.. 저도 알아요..;;

<br>

# 프로젝트를 끝내며, 종합적인 회고

----------

이번 프로젝트를 진행하며 많이 배웠고 느꼈다. 간간히 메모장에 ‘다음 번엔 이러지 말아야지’, ‘이건 좀 아쉬운데?’ 했던 것들을 적어놨다. 다음에 적는 내용들은 고쳐할 점이다.

-   나름 PM의 역할을 했다. 그나마 조금 더 아니까 프로젝트를 주도했다. 기획도, 설계도, 개발도 주도적으로 진행하면서 어떻게 리드해야하는 지 몸소 배웠다. 아직 잘은 모르겠으나 PM으로서의 역할도 나랑 잘 맞는 거 같다. 아쉬웠던 점은 처음 맡아보는 역할이었고 무엇을 어떻게 해야하는 지 잘몰라서 많이 서툴렀다. 프로젝트를 주도적으로 이끌어가는 재미를 알게되었으니 역할을 잘 수행할 수 있도록 방법론을 더 알아보도록 해야겠다.
    
-   다음 번엔 기획 단계에서 프로젝트 기간을 정해놓고 시작해야겠다. 오히려 기간이 길어지니 축쳐져서 아예 기간을 정해놓고 집중도 있게 몰아서 끝내는 게 더 완성도 있을 것 같다.
    
-   사공이 많으면 배가 산으로 가는구나 ⇒ PM다운 PM의 필요성 <br>우리는 예쁘게 디자인을 할수가 없구나 ⇒ 디자이너의 필요성
    
-   백엔드 파트를 맡았는데 spring에서 MVC 패턴을 사용하고자 무작정 따라했다. 하지만 맞게 한 건지 모르겠다. MVC2 패턴도 있던데 잘 모르고 진행했다. 잘 모르는 우리이기에 멘토가 필요하다고 느꼈다.
    
-   싹다 JPA에 의존했는데, 직접 sql query문 작성해서 **JPQL**을 이용 해야겠다.
    
-   프론트의 경우, 안드로이드에서 카카오맵을 다 연동 시켜놨는데 앱에서 지도 클러스터링이 자체적으로 지원이 안되는 걸 그제서야 알았다. (구글맵은 가능하다고 한다.) 사용자 관점의 기획이 완료된 상태에서 현실적으로 구현이 가능한 지 개발자 측면에서도 관련 기술들을 찾아보는 기획 과정의 필요성을 느꼈다. 이번 경우, 구글링을 조금만 해보면 카카오 맵과 구글 지도 중에 무엇을 선택해야할 지 정답을 알 수 있었을 것이다. 내 파트가 아닌 프론트에서 발생한 문제이긴 했지만 나에게도 충분히 일어날 수 있는 문제이기 때문에 회고한다.
    
-   직접 플로깅 하면서 필요한 기능을 직접 느껴보았으면 더 좋았을 거 같다. 실제 기능 추가 및 수정에도 좋겠지만, 제일 큰 건 보고서에도 같이 기재했으면 더 노력하는 모습 보이고 좋았을 듯? 공모전에서 보여주기 식으로 최고일텐데 아쉽다..