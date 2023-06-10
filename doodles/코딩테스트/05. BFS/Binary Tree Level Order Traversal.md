2023-06-10
16:06

해결 여부: ✅
문제: [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)
소요시간: 27m

# 풀이 계획
1. 전형적인 BFS.
2. root가 null일 때 빈 배열 반환.
3. 레벨별로 묶은 이중 배열 선언.
4. 노드와 레벨이 담길 큐로 활용할 배열 선언.
5. 큐의 길이가 0보다 클 때 while문을 돌며, result의 level 인덱스에 큐에서 빼낸 값을 넣어줌
6. node의 left, right가 있다면 레벨을 +1해서 큐에 push

# 풀이 코드 
```javascript
var levelOrder = function(root) {
    if(root === null) return []

    const result = []
    const queue = []
    
    queue.push({node: root, level: 0})

    while(queue.length > 0) {
        const {node, level} = queue.shift()

        result[level] = 
        result[level] && result[level].length > 0 
        ? [...result[level], node.val] 
        : [node.val]

        if(node.left) queue.push({node: node.left, level: level+1})
        if(node.right) queue.push({node: node.right, level: level+1})
    }

    return result
};
```
# 예상 유형
- BFS
 
# 시간 복잡도
- O(n)

# 새롭게 알게된 것
- 트리탐색 재밌군