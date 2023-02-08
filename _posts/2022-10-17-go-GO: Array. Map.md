---
title: "GO: Array, Map"
excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Go
tags:
  - [Go]

permalink: /go/array_maps/

toc: true
toc_sticky: true

date: 2022-10-17
last_modified_at: 2022-10-17
---


# GO: Array, Map

### Array

```
func main() {

	var a [5]int
	b := [5]int{1, 2, 3, 4, 5}
}
```
int형이며 길이가 5인 배열 선언해보았다.  
:= 을 통해 배열을 선언과 동시에 값을 초기화 할 수 있다.

```
var twoD [2][3]int
for i := 0; i < 2; i++ {
	for j := 0; j < 3; j++ {
		twoD[i][j] = i + j
	}
}
```
int형이며 크기가 2*3인 이차원 배열을 선언해보았다.

#

### Maps

```
func main() {

    m := make(map[string]int)

    m["k1"] = 7
    m["k2"] = 13

    fmt.Println("map:", m)

    v1 := m["k1"]
    fmt.Println("v1: ", v1)

    fmt.Println("len:", len(m))

    delete(m, "k2")
    fmt.Println("map:", m)

    _, prs := m["k2"]
    fmt.Println("prs:", prs)

    n := map[string]int{"foo": 1, "bar": 2}
    fmt.Println("map:", n)
}
```
```
make(map[키_자료형]값_자료형)
```
위와같이 make를 통해 map을 만들 수 있다.  
delete를 통해 키와 값을 한번에 삭제 할 수 있다.
