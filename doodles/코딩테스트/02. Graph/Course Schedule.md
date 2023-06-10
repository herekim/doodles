2023-06-08
16:06

해결 여부: ❌
문제: [207. Course Schedule](https://leetcode.com/problems/course-schedule/description/)
소요시간: 36m

# 풀이 계획
1. 연결 리스트로 해당 과목 Key, 선행 과목 리스트를 Value로 하는 연결 리스트를 만든다.

# 풀이 코드 
```javascript
var canFinish = function(numCourses, prerequisites) {
    let graph = new Array(numCourses);
    for(let i=0; i<numCourses; i++) {
        graph[i] = [];
    }
    
    // 그래프 구성
    for(let i=0; i<prerequisites.length; i++) {
        let course = prerequisites[i][0];
        let prerequisite = prerequisites[i][1];
        graph[course].push(prerequisite);
    }
    
    let visited = new Array(numCourses).fill(0);
    
    function isCyclic(node) {
        if(visited[node] == -1) return true;  // 노드가 순환되고 있음
        if(visited[node] == 1) return false;  // 노드가 이미 처리되었음
        
        visited[node] = -1;  // 노드 방문 시작
        for(let i=0; i<graph[node].length; i++) {
            if(isCyclic(graph[node][i])) return true;
        }
        visited[node] = 1;  // 노드 처리 완료
        return false;
    }
    
    for(let i=0; i<numCourses; i++) {
        if(isCyclic(i)) return false;  // 순환이 있는 경우 false 반환
    }
    
    return true;  // 모든 노드를 처리하고 순환을 찾지 못한 경우 true 반환
};
```
# 예상 유형
그래프, DFS
 
# 시간 복잡도
O(n)

# 새롭게 알게된 것
- 그래프는 노드와 그 노드의 연결을 표현하는 자료구조.
- 방향, 가중치에 따라 그래프의 종류를 나눌 수 있고, 그에 따른 문제도 심화 버전으로 나올 수 있다.
- 이번 문제는 그래프의 방향 처리 문제.