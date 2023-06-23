### `문제 설명`
#### English

You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure.

#### Korean

이진 검색 트리(BST)의 루트가 제공됩니다. 여기서 트리의 정확히 두 노드 값이 실수로 스왑되었습니다. 구조를 변경하지 않고 트리를 복구합니다.

### `제한 사항`

- The number of nodes in the tree is in the range [2, 1000].
- 231 <= Node.val <= 231 - 1

### `입출력 예`
### Case 1
Input: root = [1,3,null,null,2]
Output: [3,1,null,null,2]
Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.

#### Explanation
![image](https://github.com/CodingGuysGroup/Sangwoo/assets/106041072/b77b1282-605a-4e51-ad1e-cc22d7a6e6a8)

#### Case 2
Input: root = [3,1,4,null,null,2]
Output: [2,1,4,null,null,3]
Explanation: 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.

#### Explanation
![image](https://github.com/CodingGuysGroup/Sangwoo/assets/106041072/f0f2e677-4a3d-4563-b7cc-2bd3abf4ce31)

### `ANS`

----

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        arr=[]
        def order(root): # 트리 구성
            if not root:
                return 
            order(root.left)
            arr.append(root)
            order(root.right)
            return arr
        arr=order(root)
        arr_sort=sorted(arr, key=lambda x:x.val) # 각 노드의 값에 따라 정렬
        # 초기 arr = 3->2->1 순으로 구성
        # 이때 값에 따라 오름차순 정렬하고 inorder 순으로 보면
        # arr = 3-2-1, arr_sort = 1-2-3 순으로 정렬됨
        # 위에는 정렬만 됬으므로 구성도 바꿔줘야함 -> arr,arr_sort 와 비교하여 서로 같지 않으면 swap
        for i in range(len(arr)):
            if arr[i].val!=arr_sort[i].val:
                arr[i].val,arr_sort[i].val=arr_sort[i].val,arr[i].val
                return

```

### `Runtime and Memory`
![image](https://github.com/CodingGuysGroup/Sangwoo/assets/106041072/49299c02-cc30-4996-808d-55e32d4fd885)
