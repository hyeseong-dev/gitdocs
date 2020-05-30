# 영속성\(Persistence\) 정의

영속성이란 말이 가끔씩 여기저기서 튀어나올때가 있어요.   
  
이에 관해서 정리해 볼게요.   
  
추측: 영원히 존재하는 속성? 영원한 속성? 자료가 영원히 존재한다?   
어설프고 말도 안되는 1차원적인 생각을 해봤는데요. 

### **네이버**

> \(없어지지 않고 오래 동안\) 지속됨



### 위키피디아

> 영속성\(persistence\)은 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성을 의미한다. 영속성은 파일 시스템, 관계형 테이터베이스 혹은 객체 데이터베이스 등을 활용하여 구현한다. 영속성을 갖지 않는 데이터는 단지 메모리에서만 존재하기 때문에 프로그램을 종료하면 모두 잃어버리게 된다. 결국 영속성은 특정 데이터 구조를 이전 상태로 복원할 수 있게 해주어 프로그램의 종료와 재개를 자유롭게 해준다.the characteristic of data that outlives the execution of the program that created it: which is achieved in practice by storing the data in non-volatile storage such as a file system or a relational database or an object database영속성이 필요한 객체를 'persistent object'라고 하는데, 필요없는 객체는 어떻게 표기할까? 먼저 위키피디아에서는 반대 표현을 **ephemeral**이라 한다. 처음보는 형용사인데, 영속성이 불필요한 데이터 구조를 수식할 때 사용하는 것.

!\[참고1\_spring\]\[[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FweIbu%2FbtqxG6uiwp3%2F6HYEkXqKKKZy1sdmSDpvO0%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FweIbu%2FbtqxG6uiwp3%2F6HYEkXqKKKZy1sdmSDpvO0%2Fimg.png)\]

!\[참고2\]\[[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2Fc7htIz%2FbtqxGaRJptX%2FKcQuzh5LW3YWYSFgfFTsy1%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2Fc7htIz%2FbtqxGaRJptX%2FKcQuzh5LW3YWYSFgfFTsy1%2Fimg.png)\]



