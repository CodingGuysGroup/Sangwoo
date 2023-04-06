### `문제 설명`

김진영이 듣도 못한 사람의 명단과, 보도 못한 사람의 명단이 주어질 때, 듣도 보도 못한 사람의 명단을 구하는 프로그램을 작성하시오.
첫째 줄에 듣도 못한 사람의 수 N, 보도 못한 사람의 수 M이 주어진다. 이어서 둘째 줄부터 N개의 줄에 걸쳐 듣도 못한 사람의 이름과, N+2째 줄부터 보도 못한 사람의 이름이 순서대로 주어진다. 이름은 띄어쓰기 없이 알파벳 소문자로만 이루어지며, 그 길이는 20 이하이다. N, M은 500,000 이하의 자연수이다.

듣도 못한 사람의 명단에는 중복되는 이름이 없으며, 보도 못한 사람의 명단도 마찬가지이다.

### `제한 사항`

- 문자열 길이 <= 20
- N,M <= 500,000 이하 자연수

### `결과`

듣보잡의 수와 그 명단을 사전순으로 출력한다.

### `입출력 예`

|input|
|---|
|3,4||
|ohhenrie|
|charlie|
|baesangwook|
|obama|
|baesangwook|
|ohhenrie|
|clinton|

|output|
|---|
|2|
|baesangwook|
|ohhenrie|

### `ANS`

----
```
import sys
input=sys.stdin.readline
n,m=map(int,input().split())
dic={}
for _ in range(n):
    dic[input().rstrip()]=1 #듣도 못한 사람 {이름:1}로 체크
for i in range(m):
    a=input().rstrip() #보도 못한 사람 체크
    if a in dic: #보도 못한 사람 이름 중에 듣도 못한 사람 이름 존재하면 
        dic[a]+=1 #값 증가
    else: #존재하지 않으면 
        dic[a]=1 #1로 체크
cnt=0
stack=[]
for i in dic.keys():
    if dic[i]==2: #key값이 2인 듣보잡인 사람 수 체크
        cnt+=1
        stack.append(i)
stack.sort() #사전순 배열
print(cnt)
for i in stack:
    print(i)
```

```
#Counter 모듈을 이용한 다른 풀이
from collections import Counter
import sys
input=sys.stdin.readline
n,m=map(int,input().split())
stack=[]
ans=[]
for _ in range(n+m):
    stack.append(input().rstrip())
a=Counter(stack)
cnt=0
for key,value in a.items():
    if value==2:
        cnt+=1
        ans.append(key)
print(cnt)
ans.sort()
for i in ans:
    print(i)

```

### `Runtime and Memory`

![image](https://user-images.githubusercontent.com/106041072/226251442-de8ea4b1-f6cd-482a-8e6a-7441a4c2e783.png)
