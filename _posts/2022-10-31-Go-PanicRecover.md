---
title: "GO: Panic, Recover"
excerpt: "Panic과 Recover"

categories:
  - Go
tags:
  - [go]

permalink: /go/panic_recover/

toc: true
toc_sticky: true

date: 2022-10-31
last_modified_at: 2022-10-17
---
# GO: Panic Recover
## Panic

Panic은 겉으로 보기에는 아무 문제가 없지만 실행을 해보면 에러가 발생해서 프로그램을 종료하는 기능을 말한다.
```
func main() {
    panic("Error in main")
}
```
이런식으로 강제로 panic을 발생 시킬 수 있다.
<br>

### 오류와 에러의 차이
오류: 프로그램상 허용하지 않는 문법과 같은 비정상적인 상황   
```
func main(){
    var num int = 10.5 //오류
}
```
에러: 프로그램 실행되면서 논리상으로 부적합한 상황이 발생하는 것
```
func main(){
    var num1, num2 int = 10, 0
    fmt.Println(num1 / num2) //에러
}
```

## Recover
Recover은 panic을 막는 함수를 의미한다.    
panic 상황이 발생 했을때 프로그램을 종료하지 않고 예외처리를 해준다.
defer 구문과 항상 같이 사용을 해야함 
```
package main

import "fmt"

func panicTest() {
	defer func() {
		r := recover() //복구 및 에러 메시지 초기화
		fmt.Println(r) //에러 메시지 출력
	}()

	var num1, num2 int
	fmt.Scanln(&num1, &num2)
	result := num1 / num2
	fmt.Println(result)
}

func main() {
	for {
		panicTest()
		fmt.Println("Hello, world!") // panic이 발생했지만 계속 실행됨
	}
}
```
```
10과 0을 입력시
10 0
runtime error: integer divide by zero
Hello, world!

10과 1을 입력시
10 1
10
<nil>
Hello, world!
```
1. 프로그램이 종료되기 전에 실행 되어야 함으로 defer가 선언된 함수 안에서 쓰임
2. 에러 메세지를 반환함. 따라서 변수에 초기화해서 에러메세지를 출력 할 수 있음. 변수에 초기화 하지 않으면 따로 에러 메시지를 출력하지 않음