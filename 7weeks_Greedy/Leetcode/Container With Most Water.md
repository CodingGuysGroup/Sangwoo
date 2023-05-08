### `문제 설명`

#### English

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

#### Korean

길이 n의 정수 배열 높이가 제공됩니다. i번째 선의 두 끝점이 (i, 0) 및 (i, 높이[i]가 되도록 그려진 수직선은 없습니다.

x축과 함께 용기를 형성하여 용기에 물이 가장 많이 포함된 두 선을 찾습니다.

용기에 저장할 수 있는 최대 양의 물을 반환합니다.

용기를 기울여서는 안 됩니다.

### `제한 사항`

- n == height.length
- 2 <= n <= 105
- 0 <= height[i] <= 104

### `입출력 예`
### Case 1
![image](https://user-images.githubusercontent.com/106041072/236862096-a0e3d281-1ef8-4b93-b29c-b7a88677464a.png)

Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49

#### Explanation

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. 
In this case, the max area of water (blue section) the container can contain is 49.

### `ANS`

----

![image](https://user-images.githubusercontent.com/106041072/236863414-a5e64200-4282-4cb2-9be8-cedd54f04152.png)

```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        # 투 포인터 사용-> 최대한 밑변을 크게 해서 L,R을 줄여가며 최대 높이를 구하기 위해
        left=0
        right=len(height)-1 
        max_area=0
        while left<right:
            if height[left]>=height[right]: 
                max_area=max(max_area,height[right]*(right-left)) #L이 더 크므로 L보다 작은 R의 높이가 사각형의 높이가 됨
                right-=1 #L보다 R의 높이가 더 작기 때문에 최대 높이를 찾기 위해 높이가 작은 R의 위치를 왼쪽으로 당김
            else:
                max_area=max(max_area,height[left]*(right-left)) #R이 더 크므로 R보다 작은 L의 높이가 사각형의 높이가 됨
                left+=1 #R보다 L의 높이가 더 작기 때문에 최대 높이를 찾기 위해 높이가 작은 L의 위치를 오른쪽으로 당김
        return max_area

```

### `Runtime and Memory`

![image](https://user-images.githubusercontent.com/106041072/236862040-9a424ecf-b92f-4350-8d86-a05ae6bc230e.png)
