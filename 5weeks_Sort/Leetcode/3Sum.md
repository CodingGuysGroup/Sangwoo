### `문제 설명`

### English

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

### Korean

정수 배열 nums에 i!= j, i!= k, j!= k, nums[k] 및 nums[i] + nums[j] + nums[k] == 0과 같은 모든 삼중항을 반환합니다.

솔루션 세트에는 중복된 세 쌍둥이가 포함되어서는 안 됩니다.

### `제한 사항`

- 3 <= nums.length <= 3000
- -105 <= nums[i] <= 105

### `입출력 예`
### Case 1

|Input|Ouput|
|---|---|
|nums = [-1,0,1,2,-1,-4]|[[-1,-1,2],[-1,0,1]]|

#### Explanation

nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

### Case 2

|Input|Ouput|
|---|---|
|nums = [0,1,1]|[]|

#### Explanation

The only possible triplet does not sum up to 0.

### Case 3

|Input|Ouput|
|---|---|
|nums = [0,0,0]|[0,0,0]|

#### Explanation

The only possible triplet sums up to 0.

### `ANS`

----
#### Combination 모듈을 이용했으나 시간 초과 -> nC3 은 O(n!/3!*(n-3)!) 이므로 시간 너무 소모
```
from itertools import combinations
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        ans=[]
        c=list(combinations(nums,3))
        unique = []
        for i in c:
            c_sorted = tuple(sorted(list(i)))
            if c_sorted not in unique:
                unique.append(c_sorted)

        for i in unique:
            if sum(i)==0:
                ans.append(i)
        return ans
```

#### dic을 활용하여 in 함수의 시간 복잡도를 줄이고 포인터를 처음과 끝 2개로 설정하고 조건을 통해 넘기면서 시간 복잡도 줄임
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        ans=[]
        nums.sort()
        dic={}
        for i in range(len(nums)):
            min_num=i+1 # 바로 왼쪽값
            max_num=len(nums)-1 # 제일 끝값
            # min_num, max_num 내부에서 판단 
            while min_num<max_num: 
                total=nums[i]+nums[min_num]+nums[max_num] 
                if total==0: # 0으로 만족하면
                    string=[nums[i],nums[min_num],nums[max_num]] #key 값으로 넣을 문자열 선언
                    if str(string) not in dic: #dic에 없으면 넣어줌
                        dic[str(string)]=1
                        ans.append(string) #결과 리스트에 추가
                    max_num-=1 
                    min_num+=1
                elif total>0: #0보다 크면 max_num 값을 낮춤
                    max_num-=1
                else: #0보다 작으면 min_num 값을 올림
                    min_num+=1
        return ans

```

### `Runtime and Memory`

![image](https://user-images.githubusercontent.com/106041072/230755200-41cd3817-6879-4f3c-88e9-4abb6a19bcef.png)
