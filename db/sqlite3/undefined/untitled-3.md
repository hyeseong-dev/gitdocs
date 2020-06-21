# SQL문 주석

## 주석쓰는 2가지 방법  

### 1. -- 주석 

### 2. /\* 주석 \*/



### 이렇게도 되?

`/* 주석 */`와 같은 형식으로 주석을 작성하며 `/*`에서 `*/`까지 작성된 문자열은 주석이 된다.

```text
 select * from /* 주석 */ user;
```

```text
sqlite> select * from /* 주석 */ user;
1|devkuma
2|araikuma
sqlite>
```

