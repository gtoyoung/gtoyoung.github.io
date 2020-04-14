---
title: "C# Named Pipe 사용"
date: 2020-04-14 12:28:28 -0400
categories: develop
---
회사에서 Rhapsody 연동 과정에서 SCC 관련 과부하 문제가 발생하였다.  
문제는 우리가 파일 상태를 관리하는 데이터 관리 형태인 Xml파일을 로드하는 과정에서  
Rhapsody가 제한하고 있는 2G가 넘어갈 때 막무가내로 죽어버리는데 원인이 있던걸로  
파악이 되었다.

해결책을 찾아보기 위하여 Rhapsody에 Memory 관련 문의를 찾아보았다.  
우선 임시방편이지만 rhapdoy.exe 파일이 존재하는 경로에서
>editbin /LARGEADDRESSAWARE rhapsody.exe  

위의 명령어를 치게 되면 **2G에서 3G로 가용 메모리가 늘어난다**고 되어있다.  
하지만 내가 원하는건 프로그램 코드상에서 해결하고 싶었다.  


그래서 Rhapsody에 직접적으로 참조가 되어있던 dll의 역할을 최소화 하고 우리 Agent에  
부하를 맡기기로 정하였다.


방법을 찾는 중 소켓없이 프로세스간 통신이 가능한 **NamedPipe 통신**이란 것을 발견했다.  
아래는 구성한 Diagram 이다.


![image](./image/Untitled Diagram.png)

위와 같은 구성으로 개발을 진행하고 난 뒤 테스트 해보니 Rhapsody가 죽지않고 잘 수행~~
