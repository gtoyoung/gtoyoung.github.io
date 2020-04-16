---
title: "Golang을 이용한 Git Comment 조작"
date: 2020-04-16 15:05:28 -0400
categories: develop golang
---
회사업무중 Git에 대한 나의 Commit 정보를 요약하여 사용하는 경우가 있는데 항상  
visual studio나 sourcetree에 정보를 copy and paste하여 사용하기 너무 귀찮았다.  
그래서 이왕 golang을 하는거 내가 원하는대로 정보를 추출해보자 하여 시작하였다.

하지만 내가 생각한대로 바로 짜여지지 않는게 바로 코드아닌가  
예상치 못한 곳에서 난항이 생겼는데 golang에서는 c++과 같이 입력을 받는다.

```go
    fmt.Printf("텍스트를 입력해 주세요.");
    fmt.Scan(&text)
```

내가 간과한 부분은 입력 받아야 되는 값들중 Git WorkSpace 경로가 있는데 해당 경로에는 공백이 존재할 수 있다는 것이었다.  
golang 입력 부분에서 공백(whitespace)은 끝을 의미하게 된다.

golang은 생각보다 기본적인 곳에서 난항을 많이 겪게 만드는 부분이 있었다.

그래서 해당 문제에 대한 해결책은 bufio 모듈을 사용하는 것이었다.

```go
    scanner := bufio.NewScanner(os.Stdin)
    var text string
    if scanner.Scan(){
        text = scanner.Text()
    }
```

위와 같이 작성해주면 공백을 포함한 모든 글자를 입력값으로 받을 수있다.
