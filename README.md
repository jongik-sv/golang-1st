# Go언어 입문
## Go언어 들어가기
- 2007년 개발 시작, 2009년 발표, 오픈소스 프로그래밍 언어
- [로버트 그리즈머](https://en.wikipedia.org/wiki/Robert_Griesemer), [롭 파이크](https://ko.wikipedia.org/wiki/%EB%A1%AD_%ED%8C%8C%EC%9D%B4%ED%81%AC), [켄 톰슨](https://ko.wikipedia.org/wiki/%EC%BC%84_%ED%86%B0%ED%94%84%EC%8A%A8)이 개발하였다.
> - 로버트 그리즈머 : JVM 개발, javascript v8 엔진 개발
> - 롭 파이크 : Plan 9 OS개발, UTF-8 개발, 유닉스용 최초 윈도 시스템
> - 켄 톰슨 : 정규표현식, QED편집기, UTF-8 개발, B언어, C언어, 유닉스 개발
- 현재(2022년 2월 기준) 1.17.7 버전
- 온라인컴파일러 play.golang.org (https://go.dev/play/)
- 요즘 뜨는 언어, 빠르게 성장하는 언어
[zdnet 개발자가 배우고 싶은 언어 순위(2020)](https://zdnet.co.kr/view/?no=20200205112108)
    ![ex_screenshot](https://image.zdnet.co.kr/2020/02/05/firstblood_41gKQs3DW.jpg)
    
[TIOBE Index for February 2022](https://www.tiobe.com/tiobe-index/)

[2021 깃허브 언어 순위](https://json8.tistory.com/134)

[재미로 보는 언어순위](https://m.post.naver.com/viewer/postView.nhn?volumeNo=28440124&memberNo=21060)

[오버플로우 2021 순위](https://insights.stackoverflow.com/survey/2021#most-popular-technologies-language)



## Go언어의 언어적 특징
- 단순하다.(키워드가 25개 밖에 되지 않는다, 학습속도가 빠르다)
- C언어와 유사하여 배우기 쉽다.
- 클래스, 상속이 없다.
- 메서드는 있다. (구조체가 가질 수 있다)
- 인터페이스가 있다. ([덕 타이핑 방식](https://ko.wikipedia.org/wiki/%EB%8D%95_%ED%83%80%EC%9D%B4%ED%95%91))
- GC 가 있다.
- 포인터가 있다.
- 익명함수가 있다.
- 제네릭이 없다(1.18 버전 부터 제공 예정, 현재 개발 버전)
- 패키지 중심이다.(네임스페이스는 없다.)
- 여러개의 값을 리턴할 수가 있다.
- 정적타입/ 강타입 언어입니다.
- 컴파일 속도가 빠르다. (거의 인터프리터 언어 수준)
- 컴파일러 언어로 실행속도가 비교적 빠르다.( assembly > C/C++, rust > go > java > python, javascript)
- 개발 속도가 스크립트 언어에 준할 만큼 빠르다.
- 모듈이 풍부하다. (계속해서 github에 등록 되고 있다)
- 구글이 만들고 많은 대기업에서 사용중이다.(도커, 우버, 넷플릭스,카카오엔터프라이즈, 당근마켓, ....)
- 고루틴이 있다. (경량 쓰레드로 쓰레드 cost가 어마어마하게 낮다.)
- 채널이 있어서 각 고루틴간의 데이터 전송이 편리하다.
- 속도가 필요하다면 C언어를 삽입할 수 있다.(Cgo 지원)
- 접근지정자가 없다. (다만 대문자로 시작하면 외부에서 사용가능, 소문자로 시작하면 로컬에서만 사용 가능)
- [프로그래머의 평균연봉이 상위권이다.](https://thumb.zumst.com/530x0/https://static.news.zumst.com/images/98/2020/06/03/e3f785e81c884e148c8799e4eb0a9eeb.png) (java는 최하위권이다.)
- 구글 검색 시 `go` 라고 검색하지 말고 `golang`으로 검색해야 한다.



## Go 언어 단점
- 아직 성장중인 언어이다.
- 객체지향 언어이지만 객체지향으로 개발하기 힘들다.
- 현재는 없는게 많다.(제너릭, 클래스)
- 익셉션 에러 처리를 위해 코드가 지저분해질 수 있다.([2.0 버전에 추가될 예정](https://go.googlesource.com/proposal/+/master/design/go2draft.md))
- 절대적인 위치를 가진 프레임워크가 없다.(java의 스프링 같은 프레임워크가 없다)
- 포인터는 있지만 포인트 연산이 없어서 임베디드 소프트웨어에는 적합하지 않다.
- 실행파일의 크기가 최소 20MB로 임베디드 소프트웨어에 적합하지 않다.(gc, go루틴 스케줄러가 기본 포함)
- 바이너리만 배포 하므로 운영체제별/시스템별로 컴파일 해서 배포해야 한다.
---
# Go언어 찍먹
연습은 (https://go.dev/play/)에서 하면 된다.
## Hello, world!
```go
package main // main() 함수를 포함하는 패키지의 이름이 main이 아닐 경우 에러가 발생한다.

import "fmt"
  
func main() {
	fmt.Println("Hello, world!")
}
```

## Printf
```go
package main

import "fmt"

func main() {
	fmt.Printf("%d %d\n", 32, 132);
}
```

## Cgo

```go
package main

/*
#include <stdio.h>
*/
import "C"

func main() {
	C.puts("Hello world!")
}
```

## http (2.1.1/http.go)

```go
package main

import (
	"fmt"
	"net/http"
)

var c = make(chan *http.Response)

func head(url string) {
	resp, _ := http.Head(url)
	c <- resp
}

func main() {
	// HEAD 요청을 동시에 실행한다.
	go head("https://www.naver.com")
	go head("https://www.google.com")
	go head("https://golang.org")

	for i := 0; i < 3; i++ {
		resp := <-c
		if resp != nil {
			resp.Body.Close()
			fmt.Printf("%v: %s\n", resp.Request.URL, resp.Status)
			continue
		}
		fmt.Printf("%v: 연결 실패\n", resp.Request.URL)
	} 
}
```

```sh
$ go run http.go 
https://www.naver.com: 200 OK
https://www.google.com: 200 OK
https://go.dev/: 200 OK
```

## timeout (2.1.1/timeout.go)
```go
package main

import (
	"fmt"
	"net/http"
	"time"
)

func main() {
	c := make(chan string)
	go func() {
		resp, err := http.Head("https://www.google.co.kr")
		if err == nil {
			resp.Body.Close()
			c <- resp.Status
			return
		}
		c <- "연결 실패"
	}()

	// 연결 시간 초과 알림을 select로 구현할 수 있다.
	select {
	case status := <-c:
		fmt.Println(status)
	case <-time.After(2 * time.Second):
		fmt.Println("시간 초과")
	}
}

```

```sh
$ go run timeout.go
200 OK
```

---
# 변수와 상수

## 데이터 타입
### 1. 숫자타입
```
int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128 // 복소수
```
### 2. 그외 타입
```
bool
string
array
slice : go언어에서 제공하는 가변 길이 배열, 자바의 List와 유사 (사이즈를 늘리거나 줄이는 것이 가능)
struct
pointer : 메모리 주소 값을 갖는 타입(포인트 연산은 안됨)
함수 타입: 함수 포인터, 함수를 동적으로 바꿀때 유용
interface : 메서드 정의의 집합
map : key, value를 갖는 자료구조
channel : 멀티스레드 환경에 특화된 큐 형태 자료구조
```


타입의 기본값
>|Type|Zero value|
>|:---|:---|
>|Boolean|false|
>|Integer|0|
>|Floating Point|0|
>|Complex|i|
>|String|"|
>|Pointer|nil|


## 변수 선언
### 기본 형태
```go
var a int
var b int = 10 // 선언과 값 할당
```

### 타입 유추에 의한 선언 및 할당
```go
package main

import "fmt"

func main() {
	var pi = 3.14 // 변수 타입을 지정하지 않아도 유추가능

	dayPerYear := 365 // := 를 쓰면 var 를 쓰지 않아도 됨
	hello := "hello world"

	fmt.Printf("%T, %T, %T\n", pi, dayPerYear, hello)
}
```
실행결과
```
float64, int, string
```
### 타입변환
```go
a := 3 // int
var b float64 = 3.5

var c int = b // Error go언어에서는 자동 캐스팅이 되지 않음
d := a * b // Error - 다른 타입인 int 변수와 float64 연산 불가

var e int64 = 7
f := a * e // Error - a는 int, e는 int64로 연산 불가

var g int = b * 3 // Error - 실수가 정수로 자동으로 바뀌지 않음

```

맞게 고친 예제
```go
package main

import (
	"fmt"
)

func main() {
	a := 3 // int
	var b float64 = 3.5

	var c int = int(b) // float64에서 int로 변환
	d := float64(a * c)

	var e int64 = 7
	f := int64(a) * e // float64에서 int64로 변환

	var g int = int(b * 3) // 10
	var h int = int(b) * 3 // 9

	fmt.Println(a, b, c, d, e, f, g, h)
}
```
출력결과
```
3 3.5 3 9 7 21 10 9
```

## 상수
```go
const ConstValue int = 10
const ConstString string = "hello"
```

## 열거값으로 초기화

```go
const (
    A1 = iota // 0 : 0에서 시작한다
    B1 = iota // 1 : 1 증가한다
    C1 = iota // 2 : 1 증가한다
)

fmt.Println("1:", A1, B1, C1)

const (
    A2 = iota // 0 : 0에서 시작한다
    B2        // 1 : 1 증가한다
    C2        // 2 : 1 증가한다
)

fmt.Println("2:", A2, B2, C2)

const (
    A3 = iota + 1 // 1 : 1에서 시작한다
    B3            // 2 : 1 증가한다
    C3            // 3 : 1 증가한다
)

fmt.Println("3:", A3, B3, C3)

const (
    Ldate= 1 << iota //  1 : 오른쪽으로 0번 시프트 된다. 0000 0001
    Ltime            //  2 : 오른쪽으로 1번 시프트 된다. 0000 0010
    Lmicroseconds    //  4 : 오른쪽으로 2번 시프트 된다. 0000 0100
    Llongfile        //  8 : 오른쪽으로 3번 시프트 된다. 0000 1000
    Lshortfile       // 16 : 오른쪽으로 4번 시프트 된다. 0001 0000
    LUTC             // 32 : 오른쪽으로 5번 시프트 된다. 0010 0000
)
fmt.Println("Log:", Ldate, Ltime, Lmicroseconds, Llongfile, Lshortfile, LUTC)
```
---

# 표준 입출력
표준 입출력을 담당하는 fmt 패키지는 자바의 `System.out.*` 이나 C언어의 `stdio.h`와 같은 역할을 하는 패키지 이다.

패키지를 사용하기 위해서 `fmt` 패키지를 import 해야 한다.
```go
import "fmt"
```
또는
```go
import (
	"fmt"
	... // 여러 패키지를 하나의 import문으로 포함할 때는 ( )안에 나열한다.
)
```
## 표준 출력함수
|함수|설명|예|
|:---|:---|:---|
|Print()|함수의 입력값을 출력|fmt.Print(a, b, c)|
|Println()|함수의 입력값을 출력하고 개행|fmt.Println(a, b, c)|
|Printf()|서식에 맞도록 입력값을 출력|fmt.Printf("%-05d, %s, %T\n", a, b, c)|

* [서식지정자 설명 링크](http://pyrasis.com/book/GoForTheReallyImpatient/Unit41)


## 표준 입력함수
|함수|설명|예|
|:---|:---|:---|
|Scan()|표준입력에서 값을 입력 받음|fmt.Scan(&a, &b)|
|Scanf()|표준입력에서 서식에 맞게 값을 입력 받음|fmt.Scanf("%d %s\n", &a, &b)|
|Scanln()|표준입력으로 한줄을 받아서 변수에 값을 채움 (입력된 갯수가 맞지 않으면 에러 발생)|fmt.Scanln(&a, &b)|

---
# 연산자

기본적으로 C언어와 동일한 연산자를 가진다.
[go언어 연산자 설명 링크](http://pyrasis.com/book/GoForTheReallyImpatient/Unit13)

## C언어에 없는 연산자
- <- : 채널 수신 연산자, 채널에 값을 넣거나 받기 위한 연산자

## Java에 없는 연산자
- 포인터 연산자 *
- 레퍼런스 연산자 &

## 기타
- unsafe.Sizeof : 변수나 상수의 메모리 크기를 보여주는 함수

---
# 함수
## 함수 정의
```go
func Add(a, b int) int { // a, b 모두 int 형
	return a + b
}
```
func : 함수정의 키워드
Add : 함수명
a, b : 매개 변수
int : 반환 타입

## 반환 값이 여럿 일때
```go
package main

import "fmt"

func Divide(a, b int) (int, bool) {
	if b == 0 {
		return 0, false
	} 
	return a / b, true
}

func main() {
	c, success := Divide(9, 3)
	fmt.Println(c, success)
	d, success := Divide(9, 0)
	fmt.Println(d, success)
}
```
실행결과
```
3 true
0 false
```

## 변수명을 지정해 반환하기
```go
package main

import "fmt"

func Divide(a, b int) (result int, success bool) {
	if b == 0 {
		result = 0
		success = false
		return // 뒤에 변수를 쓰지 않아도 된다.
	}
	result = a / b
	success = true
	return
}

func main() {
	c, success := Divide(9, 3)
	fmt.Println(c, success)
	d, success := Divide(9, 0)
	fmt.Println(d, success)
}
```

## 가변인자 함수
```go
package main

import "fmt"

func Sum(nums ...int) int {
	sum := 0

	for _, v := range nums {
		sum += v
	}
	return sum
}

func main() {
	fmt.Println(Sum(1, 2, 3, 4))
	fmt.Println(Sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10))

}
```

## defer 지연 실행
함수 종료 시점에 실행해야 할 명령어를 등록해서 함수가 끝날때 실행 될수 있도록 하는 키워드가 `defer`이다.
예를 들어 함수에서 파일을 열고 처리 후 함수가 끝날 때 파일을 닫아 자원을 반환을 해야 한다면 아래 처럼 쓸 수 있다.

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	f, err := os.Create("test.txt")
	if err != nil {
		fmt.Println("Failed to create a file")
		return
	}
	defer fmt.Println("file close - 1")	
	defer f.Close()
	defer fmt.Println("file close - 2")
	
	...

	fmt.Println("function을 종료합니다.")
}
```
defer는 function 종료 후 역순으로 실행이 된다.

실행결과
```
function을 종료합니다.
file close - 2
file close - 1
```


## 익명함수, 함수 타입 변수

```go
package main

import (
	"fmt"
)

func main() {
	x := 10
	y := 20
	ch := make(chan int)

	// 함수를 변수에 담아서 사용 가능
	addFunction := func(a, b int) int {
		return a + b
	}
	
	// 익명함수의 실행결과를 addResult에 저장
	addResult := func(a, b int) int {
		return a + b
	}(x, y)
	
	// 익명함수를 만들어서 go루틴으로 바로 실행
	go func(a, b int) {
		ch <- a + b
	}(x, y)

	
	fmt.Printf("%T, %d, %d, %d", addFunction, addFunction(x, y), addResult, <-ch)
}

```
실행결과
```
func(int, int) int, 30, 30, 30
```
---
# if
일반적인 경우 c언어와 동일한 형태를 가진다.
다만 go 언어에는 특별한 형태의 if문도 있다.
## if 초기문; 조건문

```go
// filename, success의 변수 범위는 if문 한정이다.
if filename, success := UploadFile(); success {
	fmt.Println("Upload success", filename)
} else {
	fmt.Println("Failed to upload")
}
```
위의 코드는 아래와 같다.

```go
{ // filename과 success의 변수 스코프
	
	filename, success := UploadFile()

	if  success {
		fmt.Println("Upload success", filename)
	} else {
		fmt.Println("Failed to upload")
	}
}
```

---

# switch
c언어와 유사 하지만 다른 특징이 몇 가지 있다.

## 다른 언어와의 차이점

```go
package main

import "fmt"

func main() {
	a := "3"
	
	switch a {
	case "1":
		fmt.Println("a == 1")
	case "2", "3":
		fmt.Println("a == 2 or 3")
	case "4":
		fmt.Println("a ==  4")
	default:
		fmt.Println("a > 5")
	}
}

```
실행결과
```
a == 2 or 3
```

무엇이 C언어와 java와는 다르게 보이는가?

- string 비교가 가능하다. (java7 부터 가능하다)
- 한번에 여러값 비교가 가능하다.
- break를 쓰지 않아도 자동으로 해당 case만 처리 한다.

```go
package main

import "fmt"

func main() {
	a := 3
	
	switch true {
	case a == 1:
		fmt.Println("a == 1")
	case a >= 2 && a < 4 :
		fmt.Println("a == 2 or 3")
	case a == 4:
		fmt.Println("a ==  4")
	default:
		fmt.Println("a > 5")
	}
}

```

switch문에 true를 쓰면(true도 생략가능) 조건문(if ~ else if ~ else)를 간단하게 쓸 수 있다.

## switch문의 초기문

```go
package main

import "fmt"

func main() {
	
	
	switch a := 3;  { // 초기값을 주고 true는 생략하였다.
	case a == 1:
		fmt.Println("a == 1")
	case a >= 2 && a < 4 :
		fmt.Println("a == 2 or 3")
	case a == 4:
		fmt.Println("a ==  4")
	default:
		fmt.Println("a > 5")
	}
}
```

## break와 fallthrough 키워드
go 언어에서는 `switch` ~ `case` 문 안에서 각 case문 마지막에 `break`를 써 주지 않아도 case문을 빠져 나온다. 그런데 C언어나 java 같이 break이 없으면 아래 case문 문도 같이 실행 하고 싶다면 `fallthrough` 키워드를 써주면 된다.

```go
package main

import "fmt"

func main() {
	
	
	switch a := 1;  { 
	case a == 1:
		fmt.Println("a == 1")
		fallthrough 
	case a >= 2 && a < 4 :
		fmt.Println("a == 2 or 3")
		fallthrough
	case a == 4:
		fmt.Println("a ==  4")
	default:
		fmt.Println("a > 5")
	}
}
```
실행결과
```
a == 1
a == 2 or 3
a ==  4
```
---
# for문
go 언어에는 `while`, `do~while`문이 없다. 반복문은 모두 `for`문만 존재 한다.
## 기본형태
```go
for 초기문;조건문;후처리 {
	...
}
```
기본 형태는 다른 언어와 동일하다.
다만 초기문과 후처리를 생략할 경우 
```go
for ; 조건문 ; {
	...
}
```
위와 같이 조건문만 남을 경우 아래처럼 `;`를 모두 생략할 수 있다.
```go
for 조건문  {
	...
}

// 무한루프 (조건문 자체가 항상 true 인 경우)
for true {
	...
}

// 무한루프의 true는 생략 할 수 있다.
for {
	...
}
```

## range 순회
array, slice, map, channel 등을 순회 할 때 range를 사용하여 loop처리가 가능하다.
```go
package main

import "fmt"

func main() {

	a := []string{"a", "b", "c", "z"}
	for i, v := range a { // i는 인덱스, v는 값
		fmt.Println(i, v)
	}
}
```

---
# 배열과 slice

## 배열

### 배열의 선언과 값 할당
```go
var a[10]int32
a[0] = 1
b := [10]int{1, 2, 3, 4, 5, 6, 7}
s := [...]string{"hello", "world"} // 컴파일러가 알아서 배열 크기를 유추
var yx = [2][5]int{
	{1, 2, 3, 4, 5},
	{6, 7, 8, 9, 10},
}
```
배열에서 값이 할당이 되지 않으면 숫자는 0, string은 ""(빈문자), bool은 false로 할당이 된다.

### 배열 순회
```go
// 1차원 배열의 순회
for i := 0 ; i < len(b); i ++ {
	fmt.Println(i, b[i])
}
// 위와 같은 결과가 나온다.
for i, v := range b {
	fmt.Println(i, v)
}

// 2차원 배열의 순회
for _, y := range yx {
	for _, x := range y {
		fmt.Println(x, y)
	}
}
```


## slice
슬라이스는 배열을 랩핑(wrapping)한 자료 구조이다. java의 `List`와 유사하다.
### 배열과 슬라이스
- 공통점 : 연속된 메모리 공간을 순차적으로 이용하는 자료구조
- 차이점 : 배열은 고정된 크기, 슬라이스는 가변크기를 가진다.
- 메모리 할당 : 배열은 선언과 동시에 메모리가 할당 되지만, 슬라이스는 선언과 동시에 초기화를 하거나 `make()`함수를 통해 메모리를 할당 받아야 한다.
### 슬라이스 선언 및 메모리 할당
```go
var a []string 
a = make([]string, 5, 5) // len = 5, cap = 5로 초기화 된다.

// 선언과 할당을 동시에 
b := make([]string, 3) // cap을 초기화 하면 len과 같이 3으로 초기화 된다.

```
슬라이스 내부 구조 (https://jacking75.github.io/go_slice_array/ 참조)
![슬라이스 내부구조](https://jacking75.github.io/images/2018/golang/0006.PNG)
- ptr : 실제 데이터가 있는 배열의 주소
- len : 슬라이스의 크기
- cap : 용량(옵션항목)


그림참조 http://golang.site/go/article/13-Go-%EC%BB%AC%EB%A0%89%EC%85%98---Slice
> ![](http://golang.site/images/basics/go-slice-internal.png)

슬라이스 추가, 병합, 복사는 여기서 생략한다.
---

# map

map은 java의 맵과 거의 동일하게 `key`와 `value`로 이루어진 자료구조이다.

```go
package main

import (
	"fmt"
)

func main() {
	m := make(map[string]string)
	m["C10"] = "품질설계"
	m["M17"] = "생산관제"
	m["M20"] = "품질판정"
	m["M47"] = "조업"

	fmt.Println("C10 :", m["C10"])
	fmt.Println("M30 :", m["M30"])

	for k, v := range m {
		fmt.Println(k, v)
	}
}

```
실행결과
```
C10 : 품질설계
M30 : 
M17 생산관제
M20 품질판정
M47 조업
C10 품질설계
```
map의 값을 참조할때는 내부적으로 2개의 값을 리턴한다. 첫 번째는 value, 두 번째는 검색결과인데 있으면 true, 없으면 false를 리턴한다.

```go
package main

import (
	"fmt"
)

func main() {
	m := make(map[string]string)
	m["C10"] = "품질설계"

	value, err := m["M30"]
	fmt.Println(value, ",", err)

	value, err = m["C10"]
	fmt.Println(value, ",", err)
}


```
실행결과
```
 , false
품질설계 , true
```

---

# 구조체와 인터페이스

## 구조체 선언과 정의

```go
type Student struct {
	Name 	string
	Class 	int
	No 	int
	Score 	float64
}
```
`type` 키워드는 사용자 정의 타입을 선언할때 사용한다. 여기서는 Student라는 사용자 타입을 정의했다.

```go
var a Student
```
선언된 사용자 타입으로 변수를 생성했다.




```go
package main

import "fmt"

// struct 선언
type person struct {
	name string
	age  int
}

func main() {
	// person 객체 생성
	p := person{} // name과 age는 기본값으로 초기화 된다.

	// 필드값 설정
	p.name = "Lee"
	p.age = 10

	fmt.Println(p)

	p2 := person{"park", 19} // 객체 생성과 동시에 값 할당
	fmt.Println(p2)
	
	p3 := person{age:23, name:"kim"} // 필드명을 지정하여 할당
	fmt.Println(p3)		
}
```
실행결과
```
{Lee 10}
{park 19}
{kim 23}
```

### 구조체의 메서드
go 언어에는 class가 존재 하지 않지만 리시버(receiver)를 사용하여 메서드를 정의 할 수 있다.

```go
package main

type User struct {
	userSN int64
	name   string
	age    int16
}

func (u *User) SetName(name string) {
	u.name = name
}

// setName과 사실상 동일하다.
func SetName2(u *User, name string) {
	u.name = name
}
func (u User) Getname() string {
	return u.name
}

func (u User) PrintUser() {
	println(u.userSN, u.name, u.age)
}

func main() {

	var user1 User

	user1 = User{1, "a", 20}
	user1.SetName("jj")
	user1.PrintUser()
	SetName2(&user1, "jji")  // user1.SetName("jji") 와 동일한 역할
	user1.PrintUser()

	f1 := user1.PrintUser
	f1()
}
```
실행결과
```
1 jj 20
1 jji 20
1 jji 20
```

> value 리시버 & pointer 리시버
>- value 리시버 : call by value로 작동, 값 복사
>- pointer 리시버 : call by pointer로 작동, 포인터를 전달하여 값을 복사하지 않고 원본을 전달한다.

---
## 인터페이스
go언어에서 인터페이스는 하나의 타입이다. 그래서 `type` 키워드로 시작한다. 인터페이스는 엄밀히 말해서 값이 없는 타입이다. 이 인터페이스는 어떠한 멤버 변수도 가지지 않으며, 오직 행동만 정의한다. Go에서는 이를 통해서 다형성을 활용할 수 있다. 

```go
type DuckInterface interface {
	Fly()
	Walk(distance int) int
}
```
### 인터페이스 선언 규칙

```go
type Same interface {
	String() string
	String(int) string 	// 에러 : String() 메서드 명이 겹친다.
	_(x int)		// 에러 : 메서드는 반드시 이름이 있어야 한다.
}
```

- 메서드는 반드시 메서드 명이 있어야 한다.
- 프로토타입이 다르더라도 이름이 같은 메서드가 있으면 안된다.
- 인터페이스 안에서 메서드 구현을 포함 하지 않는다.



인터페이스도 하나의 타입이므로 `type` 키워드를 선언한다. 또한 타입이기에 변수에 담아 쓸 수 있다.

```go
package main

import "fmt"

type MyInt int
type MyFloat float64

func (i MyInt) String() string {
	return fmt.Sprintf("%d", i)
}

func (f MyFloat) String() string {
	return fmt.Sprintf("%f", f)
}

type Stringer interface {
	String() string
}

func main() {
	var i MyInt = 10
	var f MyFloat = 3.14

	fmt.Println(i.String())
	fmt.Println(f.String())

	var stringer Stringer // 인터페이스 변수

	stringer = i
	fmt.Println(stringer.String())
	stringer = f
	fmt.Println(stringer.String())

}
```

인터페이스를 쓰는 이유는??

- 구조화된 객체가 아니라 인터페이스만으로 메서드를 호출 할 수 있게 해준다.
- 코드 수정에는 닫혀 있고 확장에는 열려 있는 형태로 객체지향 프로그래밍에 아주 중요한 역할을 한다.
- 결합도를 낮출 수 있다.


## 덕 타이핑
java나 C++ 등의 언어는 인터페이스를 만들고 그 인터페이스를 클래스에서 구현 하는 식으로 프로그래밍하지만 go 언어는 타입이 가지는 메서드들에서 공통적으로 사용하는 함수들을 묶어서 인터페이스를 만든다. 말하자면 함수를 구현한 후 필요에 따라 공통적인 함수를 뽑아 그때그때 인터페이스 타입으로 만든다고 보면 된다.


# 고루틴

## 프로세스 vs 쓰레드 vs 고루틴
멀티 프로세싱 환경에서 컨텍스트 스위칭 비용을 아끼기 위해 기존 언어들은 쓰레드를 사용해 왔다. 그러나 프로세스 보다는 가볍지만 쓰레드 또한 많은 컨텍스트 스위칭 비용이 든다. go 언어에서는 쓰레드 보다 훨씬 경량화된 고루틴을 사용한다.
go 언어에서는 CPU코어(또는 CPU쓰레드) 갯수 만큼의 쓰레드를 만들어 컨텍스트 스위칭이 일어나지 않게 만들고 OS 스케줄러가 아닌 go 언어 자체의 `Golang Scheulder`를 사용한다.
보통 쓰레드의 컨텍스트 크기는 약  256kb~2MB 정도이고 고루틴은 2KB ~ 8KB 정도 이다.

## 고루틴 기본 사용방법
```go
go 함수호출
```

## 서브 고루틴이 종료될때까지 기다리기
```go
package main

import (
	"fmt"
)

func main() {
	x := 10
	y := 20

	// 익명함수를 만들어서 go루틴으로 바로 실행
	go func(a, b int) {
		fmt.Println(a + b)
	}(x, y)

	fmt.Println("프로그램을 종료합니다.")
}
```
실행 결과를 예상해보자.
.
.
.
.
.
.
.
.
.
.
.
```
프로그램을 종료합니다.
```
??????????
고루틴으로 계산한 30을 출력하는 부분은 어디 갔을까?
그 답은 go 프로그램이 실행될때 main()함수의 고루틴이 기본적으로 만들어지고 추가로 만들어진 고루틴은 서브 고루틴에서 실행이 된다. 문제는 메인 고루틴이 종료했을 때 프로그램이 종료된다는 것이다.
서브 고루틴의 결과를 기다리게 하려면 `WaitGroup` 객체를 사용하면 된다.

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	x := 10
	y := 20
	var wg sync.WaitGroup // WaitGroup을 생성

	wg.Add(1) // 1개 끝날때 까지 기다려라.
	go func(a, b int) {
		fmt.Println(a + b)
		wg.Done() // 1개 끝났다.
	}(x, y)
	wg.Wait() // 모든 고루틴이 끝날때 까지 기다린다.
	fmt.Println("프로그램을 종료합니다.")
}
```

또는 채널을 사용하여 채널에서 값을 전달하는 방법도 있다. 그 방법은 함수 챕터 "익명함수, 함수 타입 변수"에 있다.

> 모든 동시성 프로그래밍에서는 주의 해야 할 점이 있다. 여러 고루틴(다른 언어에서의 쓰레드, 프로세스)에서 동시에 같은 자원(메모리, 파일, 시스템자원)을 사용하려고 접근할 때 오류가 발생한다. 이를 해결하기 위해 뮤텍스(데드락 발생 가능)를 사용하거나 아예 영역이나 역할을 나누는 방법을 사용하면 되는데 그 방법은 심화 학습이 필요하다.


# 채널
go 언어에서는 고루틴끼리 메시지를 쉽게 전달하고 받을 수 있도록 메시지 큐 형태의 자료형인 채널을 제공한다.

## 채널 인스턴스 생성
 ```go
var message chan string = make(chan string, 10)
 ```
또는 간단하게 아래처럼 생성할 수 있다.
 ```go
message := make(chan string, 10)
 ```

여기서 10은 채널의 크기 이다. 생략을 하게 된다면 채널 크기는 1이 된다. 
채널도 하나의 큐인데 큐가 가득찬 후 추가로 채널에 값을 넣는다면 큐에서 다른 데이터가 빠져나갈 때 까지 대기한다.

데이터를 뺄때도 채널이 비어 있으면 데이터가 들어올때까지 대기 한다. 이런 특징을 이용해서 각 쓰레드간 통신뿐만 아니라 실행 순서 제어도 가능하다.

## 데이터 넣고 빼기

```go
message <- "hello" // 넣기

reciveMessage := <- message // 빼기
```

## 채널을 통한 실행 제어
```go
package main

import (
	"fmt"
	"sync"
	"time"
)

var wg sync.WaitGroup

func square(ch chan int) {

	// ch 채널이 닫힐 때까지 루프를 돈다.
	for n := range ch {
		fmt.Println(n * n)
	}
	wg.Done()
}

func main() {
	ch := make(chan int)

	wg.Add(1) // 1개 끝날때 까지 기다려라.

	go square(ch)

	for i := 0; i < 10; i++ {
		ch <- i * 2
		time.Sleep(time.Second)
	}

	close(ch) 
	wg.Wait() // 모든 고루틴이 끝날때 까지 기다린다.
	fmt.Println("프로그램을 종료합니다.")
}

```
> 여기서 close(ch)를 하지 않으면 어떻게 될까?
 
## select 
go언어에서는 여러 채널을 손쉽게 사용할 수 있도록 `select` 분기문을 제공한다. 각 채널에 값이 들어오면 해당 case가 실행된다. 
> 주의점 : default에 적절한 처리를 하지 않으면 CPU코어를 모두 점유 할 수 있으므로 주의 해야 한다.
```go
select {
case <-채널1:
	// 채널1에 값이 들어왔을 때 실행할 코드를 작성합니다.
case <-채널2:
	// 채널2에 값이 들어왔을 때 실행할 코드를 작성합니다.
default:
	// 모든 case의 채널에 값이 들어오지 않았을 때 실행할 코드를 작성합니다.
}
```

```go
package main

import (
	"fmt"
	"time"
)

func main() {
	c1 := make(chan int)    // int형 채널 생성
	c2 := make(chan string) // string 채널 생성

	go func() {
		for {
			c1 <- 10                           // 채널 c1에 10을 보낸 뒤
			time.Sleep(500 * time.Millisecond) // 100 밀리초 대기
		}
	}()

	go func() {
		for {
			c2 <- "Hello, world!"              // 채널 c2에 Hello, world!를 보낸 뒤
			time.Sleep(700 * time.Millisecond) // 500 밀리초 대기
		}
	}()

	go func() {
		for {
			select {
			case i := <-c1:                // 채널 c1에 값이 들어왔다면 값을 꺼내서 i에 대입
				fmt.Println("c1 :", i) // i 값을 출력
			case s := <-c2:                // 채널 c2에 값이 들어왔다면 값을 꺼내서 s에 대입
				fmt.Println("c2 :", s) // s 값을 출력
			case <-time.After(1 * time.Second):
				fmt.Println("시간 초과")
			default : // 과도한 CPU 점유를 막기 위해 조심
				time.Sleep(10 * time.Millisecond)
			}
		}
	}()

	time.Sleep(10 * time.Second) // 10초 동안 프로그램 실행
}
```
실행결과
```
c2 : Hello, world!
c1 : 10
c1 : 10
c2 : Hello, world!
c1 : 10
c2 : Hello, world!
c1 : 10
c1 : 10
c2 : Hello, world!
c1 : 10
...
```
