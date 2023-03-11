### `문제 설명`

### English

You are given an integer array nums with no duplicates. A maximum binary tree can be built recursively from nums using the following algorithm:


Create a root node whose value is the maximum value in nums.


Recursively build the left subtree on the subarray prefix to the left of the maximum value.


Recursively build the right subtree on the subarray suffix to the right of the maximum value.


Return the maximum binary tree built from nums.

### Korea

중복되지 않은 정수 배열 번호가 제공됩니다. 최대 이진 트리는 다음 알고리즘을 사용하여 숫자에서 재귀적으로 만들 수 있습니다:


값이 num 단위의 최대값인 루트 노드를 만듭니다.


최대 값의 왼쪽에 있는 하위 리스트에 왼쪽 하위 트리를 재귀적으로 작성합니다.


최대 값의 오른쪽에 있는 하위 리스트에 오른쪽 하위 트리를 재귀적으로 작성합니다.


숫자에서 작성된 최대 이진 트리를 반환합니다.


### `제한 사항`

- 1 <= nums.length <= 1000

- 0 <= nums[i] <= 1000

- All integers in nums are unique


### `결과`

Return the maximum binary tree built from nums.

숫자에서 작성된 최대 이진 트리를 반환합니다.

### `입출력 예`

### Case 1

![image](https://user-images.githubusercontent.com/106041072/224467006-b756569a-d272-4f57-8d4b-8d53daca284b.png)

|N|input|output|
|---|---|---|
|6|3,2,1,6,0,5|6,3,5,null,2,0,null,null,1|

#### Explanation

The recursive calls are as follow:
- The largest value in [3,2,1,6,0,5] is 6. Left prefix is [3,2,1] and right suffix is [0,5].
    - The largest value in [3,2,1] is 3. Left prefix is [] and right suffix is [2,1].
        - Empty array, so no child.
        - The largest value in [2,1] is 2. Left prefix is [] and right suffix is [1].
            - Empty array, so no child.
            - Only one element, so child is a node with value 1.
    - The largest value in [0,5] is 5. Left prefix is [0] and right suffix is [].
        - Only one element, so child is a node with value 0.
        - Empty array, so no child.

재귀 호출은 다음과 같습니다:
- [3,2,1,6,0,5]에서 가장 큰 값은 6입니다. 왼쪽 접두사는 [3,2,1]이고 오른쪽 접미사는 [0,5]입니다.
  - [3,2,1]에서 가장 큰 값은 3입니다. 왼쪽 접두사는 []이고 오른쪽 접미사는 [2,1]입니다.
    - 배열이 비어 있으므로 자식이 없습니다.
    - [2,1]에서 가장 큰 값은 2입니다. 왼쪽 접두사는 []이고 오른쪽 접미사는 [1]입니다.
        - 배열이 비어 있으므로 자식이 없습니다.
        - 요소는 하나뿐이므로 자식은 값이 1인 노드입니다.
   - [0,5]에서 가장 큰 값은 5입니다. 왼쪽 접두사는 [0]이고 오른쪽 접미사는 []입니다.
      - 요소는 하나뿐이므로 자식은 값이 0인 노드입니다.
      - 배열이 비어 있으므로 자식이 없습니다.

### Case2

![image](https://user-images.githubusercontent.com/106041072/224467255-d85645e2-f96b-4b87-bc9b-d262cd133c24.png)

|N|input|output|
|---|---|---|
|3|3,2,1|3,null,2,null,1|
----

### `ANS`

```
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
        if not nums: # 리스트가 비어 있으면 None 리턴
            return None
        A=max(nums) # 최대값 찾기
        Idx=nums.index(A) #최대값의 인덱스 찾기
        Node = TreeNode(A) #TreeNode함수 자료구조를 사용하여 최값을 노드로 선언
        Node.left=self.constructMaximumBinaryTree(nums[:Idx]) # 왼쪽 서브트리를 구성하기 위해 리스트 슬라이싱을 사용하여 재귀 사용
        Node.right=self.constructMaximumBinaryTree(nums[Idx+1:]) # 오른쪽 서브트리를 구성하기 위해 리스트 슬라이싱을 사용하여 재귀 사용
        return Node #최대 이진 트리를 완성시킨 후 노드 리턴


```

