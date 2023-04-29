### `문제 설명`

#### English

Given an integer array nums and an integer k, return the k most frequent elements. 
You may return the answer in any order.

#### Korean

정수 배열 숫자와 정수 k가 주어지면 k개의 가장 빈도가 높은 요소를 반환합니다.
답변은 어떤 순서로든 반환할 수 있습니다.

### `제한 사항`

- 1 <= nums.length <= 105
- -104 <= nums[i] <= 104
- k is in the range [1, the number of unique elements in the array].
- It is guaranteed that the answer is unique.
 
### `입출력 예`
### Case 1

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

### Case 2

Input: nums = [1], k = 1
Output: [1]

### `ANS`

----

```
from collections import Counter
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        answer=[]
        counter_list=Counter(nums).most_common(k)
        for value,frequent in counter_list:
            answer.append(value)
        return answer
```

### `Runtime and Memory`

![image](https://user-images.githubusercontent.com/106041072/235315316-36ffeef9-1bf8-4344-aec4-36ac1efc7d0c.png)
