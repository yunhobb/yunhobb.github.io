---
title: "우아한테크코스 1주차 회고"
excerpt: "회고 + 배운점"

categories:
  - Woowatech
tags:
  - [Woowatech]

permalink: /woowatech/1week

toc: true
toc_sticky: true

date: 2023-10-25
last_modified_at: 2023-10-25
---
# [우테코] 우아한테크코스 6기 프리코스 1주차 숫자야구게임 회고

## 인트로
우아한테크코스 6기 프리코스 1주차 숫자야구게임 회고입니다.

## 회고
> 작년 초 학교 과제로 요구사항을 구현한 후 순수 자바로 구현하는 것은 오랜만이다.

숫자 야구 게임은 어려서부터 친구들과 즐겨 했고 그 기억을 바탕으로 역할과 책임에 대해서 생각하며 객체지향적으로 코드를 작성하려고 고민을 많이 하였다.

일단 돌아가는 코드를 작성하자는 마음이 우선시 되어 기능명세를 간단히 하고 빠르게 구현을 들어갔습니다. 이렇게 하니 각 클래스와 메서드의 역할과 책임이 모호해지는 것을 보고 ```요구사항을 매우 세세히 구체화 하는거의 중요성을 ``` 다시 느꼈다.

리펙토링 과정에서는 최대한 비판적으로 저의 코드를 보려고 하였고 다음과 같은 의문점이 생겼다.
1. 각 요구사항의 예외 처리 위치
2. static 메서드 사용시점
3. util Class 사용
4. 메서드를 나누는 기준
5. boolean의 값을 명시적으로 더 잘 보이게 하는법
6. 메서드명과 변수명 짓기

### 1. 각 요구사항의 예외 처리 위치

이번주차 미션에서는 예외처리가 필요했다.
* 자리수가 올바른지
* 중복된 값이 입력되었는데
* 알맞은 숫자가 입력되었는지

**디스코드의 토론하기**에도 저와 같은 고민을 하는 사람들이 있었고 해당 내용을 참고해 기준을 세웠습니다. InputView는 범용적인 예외처리, domain에서는 세부적인 예외처리 

따라서
* InputView
  * 3자리 숫자를 입력하였는지 확인한다.
  * 문자가 포함되어 있는지 확인하다.
  * 재시작 입력시 1 또는 2가 입력되었는지 확인한다.
  * 재시작 입력시 문자가 포함되어 있는지 확인하다.
* domain
  * 입력된 값의 각 자리수가 1 ~ 9인지 확인한다.
  * 중복된 값이 입력되었는지 확인하다.

로 기준을 나눴다.

### 2. static 메서드 사용시점, 3. util Class 사용
첫번째 구현시 InputView와 OutputView의 메서드를 static으로 선언을 했다. 그 이유는 InputView와 OutputView는 인스턴스 생성이 불필요하다 생각을 하여서 해당 방식으로 구현을 하였다. 하지만 적절한 이유가 아니라는 생각을 하였고 찾아본 후 아래와 같은 기준을 만들었다.
* ```반복되는 메서드```를 사용하는 시점에 사용한다. (ex. util class)
* 정적 펙토리 메서드에 사용한다.
* 특별한 디자인 패턴 사용시 사용한다.
* enum에서 값 처리 할 때 사용한다.

추후에 경험을 통해 더 추가하겠다.

### 5. 메서드를 나누는 기준
처음 작성한 코드에서는 뭔가 코드를 자연스럽게 읽기 어려웠다. 그리하여 이유를 고민하였고 메서드 분리가 제대로 이루어지지 않았다고 생각이 되었다. 


[[Tecoble]하나의 메서드는 하나의 기능을 수행하자
](https://tecoble.techcourse.co.kr/post/2020-05-10-single-job-method/)

블로그를 보고 메서드를 기능 단위로 즉 하나의 역할만하게 수정을 하였다.

### 5. boolean의 값을 명시적으로 더 잘 보이게 하는법
메서드 중 결과 값이 boolean으로 반환되는 메서드는 ```isXXXXX```식으로 네이밍을 하였다. 
조건문의 제약식 또한 메서드를 분리하여 개선하였다.

### 6. 메서드명과 변수명 짓기
[[Tecoble]좋은 코드를 위한 자바 메서드 네이밍](https://tecoble.techcourse.co.kr/post/2020-04-26-Method-Naming/)

[[Tecoble]좋은 코드를 위한 자바 변수명 네이밍](https://tecoble.techcourse.co.kr/post/2020-04-24-variable_naming/)

위 두 블로그를 보고 확실히 네이밍을 잘한 코드는 눈에 바로 들어오는게 느껴졌다.

## 마무리
코드를 제출한 후 메서드 중 매개변수가 ```List<Integer>```로 들어가 있는 것을 확인했다. 이부분을 일급 컬랙션으로 빼면 좋았을까란 개선점이 보였다.

또 테스트 코드를 작성하던 잘못된 첨을 찾았다. 랜덤한 수를 생성하는 로직을 Util class로 작성해 생성자에서 수를 초기화하니 테스크 코드에서 임의의 값을 생성하지 못해 결국 해당 부분은 테스트 코드를 작성하지 못했다. 아직 이 부분은 내 자신이 테스트 코드를 작성하는 방법을 잘 몰라서 인지 아니면 잘못된 설계인건지 명확한 판단이 안서 조금 더 찾아보려고 한다.

## 앞으로
더 자연스럽게 읽히는 코드를 작성하려고 하다보니 무엇을 하든간에 코드의 방향성을 생각하게 되어 신선한 경험이었습니다. 1주차가 마무리 되었으니 디스크 커뮤니티를 통해 다양한 사람들에게 저의 코드를 리뷰 받고 제가 보지 못한 개선점을 찾고 싶습니다. 또 코드의 개선점을 찾을 때 디스코드의 함께 나누기에 올라온 게시물을 많이 보았는데, 블로그는 대부분 Tecoble이었고 우테코에 들어가 위와 같은 내용을 직접 사람들과 대화를 통해 나누어 성장을 도모하고 싶다는 생각이 많이 들었습니다.

[코드 링크](https://github.com/yunhobb/java-baseball-6/tree/yunhobb)