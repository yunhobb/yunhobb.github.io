---
title: "Early Return Pattern"
excerpt: "else를 쓰지 말라고? "

categories:
  - Java
tags:
  - [Java]

permalink: /java/early-return

toc: true
toc_sticky: true

date: 2023-08-01
last_modified_at: 2023-08-01
---
# Return Early Parttern !

평상시 코드를 작성할 때 else 또는 else if 를 자주 사용했던거 같다.

```java
public String returnStuff(SomeObject argument, SomeObject argument2){
	if(argument1.isValide()){
        if(argument2.isValide()){
        	SomeObject otherVal1 = doSomeStuff(argument1, argument2)
            
            if(otherVal1.isValid()){
            	someObject otherVal2 = doAnothreStuff(otherVal1)
                
                if(otherVal2.isValide()){
                	return "Stuff";
                 }else{
                 	throw new Exception();
                 }
            }else{
            	throw new Exception();
            }
        }else{
        	throw new Exception();
        }
    }else{
    	throw new Exceptioon();
    }
}
}
```
인터넷에서 else를 남발하는 예시를 가져왔다.

위 코드에서 알 수 있는 점은 

* if 조건문의 block이 길 경우 코드를 알아보기 힘들다.
* 예상 결과를 얻기 위해서는 중첩된 if를 따라 가야만 한다.
* 만약 else이 실행문을 종료 시키지 않는다면. 나머지 코드를 실행되고 이로인해 또다른 에러가 발생할 수 있다.
* Else Considerd Smelly: 조건문이 복잡하면 else인 경우를 찾는 것은 두배로 힘들다.
* Arrow Anti Pattern: 조건문의 중첩으로 인해 코드 모양이 화살처럼 된다.

# Return Early 
> Return early는 함수는 메소드를 작성하는 방식으로, 예상되는 긍정 결과가 함수의 끝에서 리턴되게 하고 조건이 맞지 않는 경우 나머지 코드는 예외를 return 하거나 throw해서 실행을 종료한다.
이러한 방식은 if 조건문으로 에러 처리나 적절한 예외를 반환하거나 throwing하여 함수의 실행문을 끝내는 방식으로 수행된다.

위에 코드를 **Return Early** 패턴을 적용하면 
```java
public String returnStuff(SomeObject argument1, SomeObject argument2){
	if(!argument1.isValid()) {
    	throw new Exception();
    }
    
    if(!argument2.isValid()) {
    	throw new Exception();
    }
    
    SomeObject otherVal1 = doSomeStuff(argument1, argument2);
    
    if(!otherVal1.isValid()) {
    	throw new Exception();
    }
    
    SomeObject otherVal2 = doAnotherStuff(otherVal1);
    
    if(!otherVal2.isValid()) {
    	throw new Exception();
    }
    
    return "Stuff";
}
```
위의 코드에서 알 수 있는 사항
* linerly하게 읽을 수 있다.
* 예상되는 긍정 결과는 함수의 끝에서 빨리 찾을 수 있다.
* 위와 같이 작성하면 에러를 먼저 잡고 그 다음 불필요한 버그를 피하면서 안전하게 비지니스 로직을 구현할 수 있다.
* fail-fast 사고방식은 TDD와 유사해서 테스트에도 용이하다.
* 함수에서 에러가 발생시 즉시 종료되므로 의도하지 않은 코드가 실행될 가능성을 피할 수 있다.

# 결론 
코드를 작성하면서 자연어 처럼 읽히는 코드를 작성하려고 생각을 한다.  **return early** 패턴은 함수가 혼잡해지는것을 방지하는 훌륭한 방법이다.

# Reference
* [https://medium.com/swlh/return-early-pattern-3d18a41bba8](https://medium.com/swlh/return-early-pattern-3d18a41bba8)
* [https://libertegrace.tistory.com/entry/Coding-Style-Return-Early-Pattern](https://libertegrace.tistory.com/entry/Coding-Style-Return-Early-Pattern)