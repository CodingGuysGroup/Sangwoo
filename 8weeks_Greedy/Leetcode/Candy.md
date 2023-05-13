### `문제 설명`

#### English

There are n children standing in a line. Each child is assigned a rating value given in the integer array ratings.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

Return the minimum number of candies you need to have to distribute the candies to the children.

#### Korean

아이들이 줄을 서 있습니다. 각 하위 항목에는 정수 배열 등급으로 지정된 등급 값이 할당됩니다.

귀하는 다음과 같은 요구 사항에 따라 이 어린이들에게 사탕을 제공하고 있습니다:

- 각각의 아이들은 적어도 하나의 사탕을 가지고 있어야 합니다.
- 등급이 높은 아이들은 이웃보다 사탕을 더 많이 받습니다.

아이들에게 사탕을 나눠주기 위해 필요한 최소한의 사탕을 돌려주세요.

### `제한 사항`

- n == ratings.length
- 1 <= n <= 2 * 104
- 0 <= ratings[i] <= 2 * 104

### `입출력 예`
### Case 1

|input|output|
|---|---|
|ratings = [1,0,2]|5|

#### Explanation

You can allocate to the first, second and third child with 2, 1, 2 candies respectively.

#### Case 2

|input|output|
|---|---|
|ratings = [1,2,2]|4|

### Explanation

You can allocate to the first, second and third child with 1, 2, 1 candies respectively.
The third child gets 1 candy because it satisfies the above two conditions.

### `ANS`

----

```
class Solution:
    def candy(self, ratings: List[int]) -> int:
        candy_list=[1]*len(ratings) #최소 한개씩은 가져야하므로 1로 할당
        #좌우에 대해 큰 ratings이 높은것을 확인하여 캔디를 더 가져야하므로 각각 왼쪽, 오른쪽으로 가면서 ratings 확인 후 캔디를 증가하는 방식
        #오른쪽으로 가면서 ratings 확인 후 캔디 주기
        for i in range(1,len(ratings)):
            if ratings[i-1]<ratings[i]:
                candy_list[i]=candy_list[i-1]+1
        #왼쪽으로 가면서 ratings 확인 후 캔디 주기 이때 이미 오른쪽으로 가면서 완료된 값과 비교하기 위해 max 사용
        for i in range(len(ratings)-1,0,-1):
            if ratings[i-1]>ratings[i]:
                candy_list[i-1]=max(candy_list[i-1],candy_list[i]+1)
        return sum(candy_list)
            
```

### `Runtime and Memory`
![image](https://github.com/CodingGuysGroup/Sangwoo/assets/106041072/e07d4f9f-4894-4355-939d-37714b802a6d)
