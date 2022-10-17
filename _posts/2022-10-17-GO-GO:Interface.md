---
title: "[포스팅 예시] 이곳에 제목을 입력하세요"
excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Go
tags:
  - [go]

permalink: /go//

toc: true
toc_sticky: true

date: 2022-10-17
last_modified_at: 2022-10-17
---


# GO: Interface, Struct


## Interface

```
type geometry interface {
	area() float64
	perim() float64
}
```
type문을 사용하여 정의한다.  
인터페이스가 갖는 모든 메서드들을 구현하면 된다.


## Struct
```
type rect struct {
	width, height float64
}
type circle struct {
	radius float64
}
```
인터페이스와는 다르게 메서드를 가질 수 없고 필드 데이터만을 선언 해줄 수 있다.

```
func (r rect) area() float64 {
	return r.width * r.height
}
func (r rect) perim() float64 {
	return 2*r.width + 2*r.height
}
func (c circle) area() float64 {
	return math.Pi * c.radius * c.radius
}
func (c circle) perim() float64 {
	return 2 * math.Pi * c.radius
}
```
Rect 타입에 대한 Shape 인터페이스를 구현하고   
Circle 타입에 대한 area, perim 인터페이스를 구현한 상태이다.