---
title: "GO: Gin Web Framework"
excerpt: "Gin"

categories:
  - Go
tags:
  - [go]

permalink: /go/ginwebframework/

toc: true
toc_sticky: true

date: 2022-11-07
last_modified_at: 2022-11-07
---
# GO: Gin Web Framework (Restful API)
go 언어를 쓰는 마이크로 웹 프레임워크이다.

<br>

*** 

## Quickstart

```
$ go mod init example/web-service-gin
```
go mod init 명령어를 통해 종속성관리와 패키지를 설치합니다.


*** 

## 구조체 선언

```
type album struct {
    ID     string  `json:"id"`
    Title  string  `json:"title"`
    Artist string  `json:"artist"`
    Price  float64 `json:"price"`
}
var albums = []album{
    {ID: "1", Title: "Blue Train", Artist: "John Coltrane", Price: 56.99},
    {ID: "2", Title: "Jeru", Artist: "Gerry Mulligan", Price: 17.99},
    {ID: "3", Title: "Sarah Vaughan and Clifford Brown", Artist: "Sarah Vaughan", Price: 39.99},
}
```
위와 같이 구조체를 선언하고 선언한 구조체에 데이터를 넣는다.   

구조체의 필드 끝에 역따옴표가 붙는 이유:  
Raw string은 보통 JSON 형식의 String을 처리할 때 종종 사용한다. JSON key, value가 일반적으로 쌍따옴표로 이루어진 string이기 때문에 이를 Interpreted string으로 나타내게 되면 쌍따옴표 구분을 명확하게 해줘야 해서 번거롭기 때문이다.
***

## 함수
파일끝에 함수를 선언하는게 좋지만 Go는 어디에 위치해도 상관없다.
### 
```
func getAlbums(c *gin.Context) {
    c.IndentedJSON(http.StatusOK, albums)
}
```
 
gin.Context : json의 유효성을 검사하고 직렬화를 담당   
Context.IndentedJSON: json을 직렬화하고 응답을 추가하기 위해서 쓴다
<br></br>

```
func postAlbums(c *gin.Context) {
	var newAlbum album

	if err := c.BindJSON(&newAlbum); err != nil {
		return
	}

	albums = append(albums, newAlbum)
	c.IndentedJSON(http.StatusCreated, newAlbum)
}
```
Context.BindJSON: request body 를 newAlbum 변수에 맵핑


<br></br>
```
func getAlbumByID(c *gin.Context) {
	id := c.Param("id")

	for _, a := range albums {
		if a.ID == id {
			c.IndentedJSON(http.StatusOK, a)
			return
		}
	}

	c.IndentedJSON(http.StatusNotFound, gin.H{"message": "album not found."})
}
```
Context.Param: URL 로 부터 id path parameter을 추출
***

## main 함수

```

func main() {
	router := gin.Default()
	router.GET("/albums", getAlbums)
	router.POST("/albums", postAlbums)
	router.GET("/albums/:id", getAlbumByID)

	router.Run("localhost:8080")
}
```
Default: Gin에서 기본적인 라우터를 생성

***

## 결과

<img width="1106" alt="image" src="https://user-images.githubusercontent.com/87285536/200311887-b503f62f-1573-4d8e-8058-1c446c39a12a.png">

<img width="1106" alt="image" src="https://user-images.githubusercontent.com/87285536/200312025-8e2c6ba6-239d-4d38-a6c8-9ef3dd86d6c7.png">

<img width="1097" alt="image" src="https://user-images.githubusercontent.com/87285536/200312162-00b0f92b-2851-4c43-9318-7f093883bc29.png">
<img width="1104" alt="image" src="https://user-images.githubusercontent.com/87285536/200312797-b7bae787-0411-49d2-acea-548286901df0.png">
