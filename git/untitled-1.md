# Untitled

## 브렌치 

git에서 가장 중요한 부분이자 핵심입니다.   
브렌치는 나무의 가지를 의미하고 이. 즉 나무의 가지처럼 여러가지 원류에서 뻗어 나간다는  느낌?이라고 보면 되요.   
  
여러분이 report.xsl --&gt; report1.xsl --&gt; report2.xsl 파일로 순차적으로 네이밍을 해서 저장할 수 있어요.   
그런데 특정한 상황\(고객 전달\)에서는 report2\_client.xsl이라는 파일도 만들어 줘야해요.   
그런데 여러분이 report3.xsl, report4.xsl이라는 개발자가 만드는 파일을 만들어 줘야해요.   
  
즉 가지가 분화되어 나간다는거조. 이떄 나무의 가지개념이 도입된게 git의 branch에요. 

```text
                           |-->report2_client.xsl--> report3_client.xsl--
                           |                                            |                                           
report.xsl -> report1.xsl -> report2.xsl -> report3.xsl-> report4.xsl ---->report5.xsl -> report6.xsl
```

더불어 추후 고객용 파일에서 수정되거나 더해진 사항이 report3\_client파일과 report4.xsl이 더해져서 report5.xsl파일로 만들어져야 하는 상황도 있을 수 있어요.  
  
물론 합치는 경우도 있고 합치지 않는 경우도 있어요.   


3번째줄은 원래 작업 공간\(원 브렌치\)이고 고객용으로 제공된 브랜치는 1번째줄이에요.   
사실 report1.xsl  
  
  
출처: [https://opentutorials.org/course/2708/15259](https://opentutorials.org/course/2708/15259)

