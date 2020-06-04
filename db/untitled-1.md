# Untitled

sqlite를 실습하기 위해 가볍게 파이썬 파일을 아래와 같이 작성해 볼게요.

{% code title="" %}
```text
import sqlite3

print ('hello world')

# DB 연결
conn = sqlite3.connect('my.db')
cursor = conn.cursor()

# INSERT 문
memo = '1234'
cursor.execute('INSERT INTO memo(no, memo) VALUES(?, ?)', (10, memo)) 

# SELECT 문 - 한개
cursor.execute('SELECT * FROM memo WHERE no=1')
memo = cursor.fetchone()
print('memo(%s, %s)' % (memo[0], memo[1]))

# SELECT 문 - 리스트
cursor.execute('SELECT * FROM memo')
memos = cursor.fetchall()
for memo in memos:
    print('memo(%s, %s)' % (memo[0], memo[1]))
```
{% endcode %}

## 모르는 용어, 메소드

원인 : 

1. cursor\(\)
2. execute\(\)
3. fetchone\(\)
4. fetchall\(\)
5. connect\(\)

리스트의 특정한 index나 혹은 리스트 index 전체를 가져올때 가져온다. 

fetchall\(\)





