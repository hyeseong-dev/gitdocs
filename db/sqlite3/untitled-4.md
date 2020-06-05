# SQLite 키워드 유의사항

###  SQLite 키워드 유의사항 

키워드, 예약어 = SELECT, TABLE과 같이 기능적 역할을 갖추고 있어. 변수로 사용할 수 없어요.   
  
테이블명이나 데이터베이스명은 식별자라고 한다. 식별자는 알파벳이나 숫자 등을 조합하여 지정할 수 있다. 예를 들어 booktable이나 name 가능하다. 단, SQLite의 키워드는 그대로 식별자로 사용할 수 없다. 예를 들면 select를 테이블명으로 사용하려고하면 오류가 발생한다.



```text
create table select(id, name);
```

```text
sqlite> create table select(id, name);
Error: near "select": syntax error
sqlite>
```

#### 그래도 굳이 키워드를 식별자로 사요하려면?

아래 규칙을 사용해보세요. 

```text
'keyword'
"keyword"
[keyword]
`keyword`
```

1. 따옴표 

```text
create table 'select'(id, name);
```

쌍따움표\("\), 대괄호 \(\[\]\), 억음 부호\(\`\)로 키워드를 둘러싼 경우 식별자로 처리된다. 또한 문자열을 작성해야 곳에 쌍따움표로 둘러싸서 식별자를 작성하면 문자열로 처리된다.

```text
create table "select"(id, name);
```

```text
sqlite> create table "select"(id, name);
Error: table "select" already exists
sqlite> drop table 'select';
sqlite> create table "select"(id, name);
sqlite> 
```

여기서 대괄호는 Access 또는 SQL Server에서 사용되는 방식이고 엄음 부호는 MySQL에서 사용되는 방식디다. 이 두 가지 방식은 각각의 데이터베이스와의 호환성을 위해 준비되어 있는 것이므로, 일반적으로 따움표 또는 쌍따움표로 사용하도록 한다



### Keywork List

| ABORT | ACTION | ADD | AFTER | ALL |
| :--- | :--- | :--- | :--- | :--- |
| ALTER | ANALYZE | AND | AS | ASC |
| ATTACH | AUTOINCREMENT | BEFORE | BEGIN | BETWEEN |
| BY | CASCADE | CASE | CAST | CHECK |
| COLLATE | COLUMN | COMMIT | CONFLICT | CONSTRAINT |
| CREATE | CROSS | CURRENT | CURRENT\_DATE | CURRENT\_TIME |
| CURRENT\_TIMESTAMP | DATABASE | DEFAULT | DEFERRABLE | DEFERRED |
| DELETE | DESC | DETACH | DISTINCT | DO |
| DROP | EACH | ELSE | END | ESCAPE |
| EXCEPT | EXCLUSIVE | EXISTS | EXPLAIN | FAIL |
| FILTER | FOLLOWING | FOR | FOREIGN | FROM |
| FULL | GLOB | GROUP | HAVING | IF |
| IGNORE | IMMEDIATE | IN | INDEX | INDEXED |
| INITIALLY | INNER | INSERT | INSTEAD | INTERSECT |
| INTO | IS | ISNULL | JOIN | KEY |
| LEFT | LIKE | LIMIT | MATCH | NATURAL |
| NO | NOT | NOTHING | NOTNULL | NULL |
| OF | OFFSET | ON | OR | ORDER |
| OUTER | OVER | PARTITION | PLAN | PRAGMA |
| PRECEDING | PRIMARY | QUERY | RAISE | RANGE RECURSIVE |
| REFERENCES | REGEXP | REINDEX | RELEASE | RENAME |
| REPLACE | RESTRICT | RIGHT | ROLLBACK | ROW |
| ROWS | SAVEPOINT | SELECT | SET | TABLE |
| TEMP | TEMPORARY | THEN | TO | TRANSACTION |
| TRIGGER | UNBOUNDED | UNION | UNIQUE | UPDATE |
| USING | VACUUM | VALUES | VIEW | VIRTUAL |
| WHEN | WHERE | WINDOW | WITH | WITHOUT |

이 중에 일부 키워드는 특히 따움표나 쌍따움표 등으로 둘러싸지 않아도 식별자로 사용할 수 있는 것도 있다. 단지, 키워드를 그대로 식별자로 사용하면 알아 보기 어렵기 때문에 그다지 바람직한 방법은 아니다.

테이블 등을 생성 때에 알 수 없는 에러가 발생하면 테이블명과 컬럼명이 키워드되어 있는지 확인하여 보길 바란다.



Resource : [http://www.devkuma.com/books/pages/1263](http://www.devkuma.com/books/pages/1263)

