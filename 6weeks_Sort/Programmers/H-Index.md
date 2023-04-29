### `문제 설명`

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

### `제한 사항`

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

### `결과`

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

### `입출력 예`
### Case 1
|citations|return|
|---|---|
|[3, 0, 6, 1, 5]|3|

#### Explanation

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

### `ANS`

----

```
def solution(citations):
    citations.sort() 
    max_value=citations[-1] #최대값 저장
    answer=0
    if citations[0]>=len(citations): #제일 작은 값이 전체 논문 횟수 보다 큰 경우 ex) [10,10,10]
        answer=len(citations) # 논문 횟수를 리턴
        return answer
    for i in range(max_value+1): 
        first=0 # 첫번째 조건을 만족하는 횟수 (h번 이상 인용된 논문이 h편 이상인 경우)
        second=0 # 두번째 조건을 만족하는 횟수 (나머지 논문이 h번 이하 인용된 경우)
        for j in citations: #조건 카운트
            if j>=i:
                first+=1
            if j<=i:
                second+=1
        if first>=i and second>=0: #h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 0보다 크면 됨
            answer=i #for 문 돌면서 알아서 최대값으로 설정됨
        else:
            return answer # 위 조건 만족하지 못하면 바로 리턴하여 시간 절약
    return answer # 한번 더 리턴한 이유는 [0,0,0,0,0,0] 처럼 위 조건을 계속 만족하여 else 문의 리턴이 진행되지 않는 경우를 고려하여 리턴 한번 더 함
            

```

#### 다른 풀이 - 참조
```
def solution(citations):
    citations.sort(reverse=True) # ex) [3,0,3,6,1,5] => [6,5,3,3,1,0]
    #list(enumerate(citations, start=1)) => [(1,6),(2,5),(3,3),(4,3),(5,1),(6,0)]
    #밑에 그래프를 보면 인덱스가 증가함에 따라 인용횟수는 감소하는 것을 알 수 있음 -> 교차하는 지점이 정답
    #교차하는 부분을 파악하기 위해 각 튜플에서 최대값은 버리고 최솟값만 살림
    #list(map(min,enumerate(citations, start=1))) => [1,2,3,3,1,0]
    # max 함수 처리를 하면 교차 지점의 최대를 구할 수 있음 [1,2,3,3,1,0]-> 3 
    answer = max(map(min, enumerate(citations, start=1)))
    return answer
```
![image](https://user-images.githubusercontent.com/106041072/235316906-f48418d2-f335-4036-b8fa-c6012335a564.png)

### `Runtime and Memory`

![image](https://user-images.githubusercontent.com/106041072/235314102-3b0280f7-35e1-4b80-8866-29fbaa7a15b5.png)
