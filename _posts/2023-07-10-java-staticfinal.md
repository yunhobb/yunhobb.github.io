---
title: "final이 뭐야?"
excerpt: "자바에서 final 키워드"

categories:
  - Java
tags:
  - [Java]

permalink: /java/final

toc: true
toc_sticky: true

date: 2023-07-09
last_modified_at: 2023-07-09
---
# 발단
<img width="491" alt="image" src="https://github.com/yunhobb/yunhobb.github.io/assets/87285536/a723cf58-4864-4c64-959a-deb5a74759c9">

프로젝트를 진행하던 중 팀원분의 코드를 보니 매개변수를 입력받는 곳에 final이 선언이 되어있는 것을 보았다.

final 키워드를 평상시에 의식하지 않고 사용도 잘하지는 않은거 같아 이번기회에 알아가면 좋을거 같아 간단하게 정리를 해보려고 한다.

# 그래서 final이 뭐지? 

[사전]:  final 최종적인

사전을 보면 위와 같이 작성된 것을 알 수 있다.

단어 뜻처럼 해당 변수에 값이 최종적으로 저장되면 수정이 불가능함을 뜻한다.

final 필드 값에 값을 주는 방법은 두 가지가 있다.
```java
public class Game{

    final int hp = 100
    int mp;
    
    public game(final int mp){
        this.mp = mp;
    }
}
```
1. hp처럼 선언과 동시에 값을 주는 방법이 있고
2. mp처럼 객체를 생성할 떄 생성자를 통해 값을 저장해 주는 방법이 있다.
   
**정리하면** 

final : 한 번 값이 정해지고 나면 값을 바꿀 수 없는 필드를 뜻한다.

# 처음으로 가서 
그럼 결국 왜 매개변수를 받는 부분에 ```final```을 작성해 주었냐?


**final** 키워드를 사용하는 것은 가변성을 제한하고 코드의 안정성을 높이는 데 도움이 된다. 또한 다른 개발자들이 해당 변수를 실수로 변경하지 않도록 명시적으로 표시하는 역할도 한다.

기능적인 부분도 있겠지만 명시적으로 나타내주기 위해서 작성을 해준다고 이해를 하면 될 거 같다.

요즘 코드를 작성하면서 남들이 어렵지 않게 받아드릴 수 있는 코드의 작성이 중요하다는 것을 느끼고 있다. 

이어서 static과 static final키워드를 정리해 보겠다.
