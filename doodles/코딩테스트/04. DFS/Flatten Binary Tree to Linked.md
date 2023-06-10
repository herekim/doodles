2023-06-10
15:06

해결 여부: 🥑
문제: [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)
소요시간: 24m

# 풀이 계획
1. root가 null이라면 그냥 반환
2. root.left가 존재한다면 root.right로 붙여주고, root.left를 null로 변경
3. 기존 root.right는 root.left의 가장 오른쪽 끝 node의 자식 node도 붙여줌
4. 다시 root.right를 flatten 함수에 넘겨서 반복
# 풀이 코드
```javascript
var flatten = function(root) {
    if(root === null) return

    if(root.left) {
        const right = root.right
        root.right = root.left
        root.left = null

        let node = root.right
        while(node.right) {
            node = node.right
        }
        node.right = right
    }

    flatten(root.right)
}
```
# 예상 유형
- DFS
 
# 시간 복잡도
- O(1)

# 새롭게 알게된 것
-