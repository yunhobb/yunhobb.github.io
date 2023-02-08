---
title: "GO: Hello World!"
excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Go
tags:
  - [Go]

permalink: /go/helloworld/

toc: true
toc_sticky: true

date: 2022-07-24
last_modified_at: 2022-07-24
---


# GO: Hello World!

GDSC스터디에서 go언어 스터디를 시작하게 되었다. 

기본적인 소스코드이다.

```
package main

import "fmt"

func main() {
	fmt.Println("hello world")
}
```
#

```
import 'fmt'
```
println을 쓰기 위해 모듈을 불러왔다.  

#### 실행 하는법 
```
$ go run hello.go
```

#### binary파일로 변환해서 실행 할 수 있다. 
```
$ go build hello.go 
$ ./hello.go
```
