### `문제 설명`

#### English

Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

An integer a is closer to x than an integer b if:
- |a - x| < |b - x|, or
- |a - x| == |b - x| and a < b

#### Korean

정렬된 정수 배열 배열이 주어지면 두 정수 k와 x가 주어지면 k개의 가장 가까운 정수를 배열의 x로 반환합니다. 결과도 오름차순으로 정렬해야 합니다.

다음과 같은 경우 정수 a는 정수 b보다 x에 가깝습니다:

- |a - x| < |b - x|, 또는
- |a - x| == |b - x| 와 a < b

### `제한 사항`

- 1 <= k <= arr.length
- 1 <= arr.length <= 104
- arr is sorted in ascending order.
- -104 <= arr[i], x <= 104

### `결과`

The result should also be sorted in ascending order.

### `입출력 예`
### Case 1

|input|output|
|---|---|
|arr = [1,2,3,4,5], k = 4, x = 3|[1,2,3,4]|

### Case 2

|input|output|
|---|---|
|arr = [1,2,3,4,5], k = 4, x = -1|[1,2,3,4]|

### `ANS`

----

```
import heapq
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        heap=[]
        ans=[]
        for i in range(len(arr)):
            heapq.heappush(heap,(abs(arr[i]-x),i)) #튜플 형태로 x와 떨어진 거리값과 해당 인덱스를 저장
        for _ in range(k):
            ans.append(arr[heapq.heappop(heap)[1]]) #k개만큼 해당 인덱스의 값을 가지는 arr 리스트를 뽑아 ans에 추가
        ans.sort() #오름차순 정렬
        return ans

```

### `Runtime and Memory`

![image](https://user-images.githubusercontent.com/106041072/229699811-1ada2d3f-f810-4a68-9df9-6ebdc6583118.png)
