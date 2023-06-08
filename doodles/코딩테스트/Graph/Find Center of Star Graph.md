2023-06-08
15:06

해결 여부: ✅
문제: [1791. Find Center of Star Graph](https://leetcode.com/problems/find-center-of-star-graph/description/)
소요시간: 24m

# 풀이 계획
1. edges를 순회한다.
2. 중복 제거를 위해 Set을 만들고, 만약 check 셋에서 이미 존재하는 edge가 있다면 바로 반환한다.
# 풀이 코드 
```javascript
var findCenter = function(edges) {
    const check = new Set()
    for(const [a,b] of edges) {
        if(check.has(a)) {
            return a
        }
        if(check.has(b)) {
            return b
        }
        check.add(a)
        check.add(b)
    }
};
```
# 예상 유형
그래프
 
# 시간 복잡도
O(n)

# 새롭게 알게된 것
- 중심부의 조건을 알고있다면 간단하게 풀 수 있는 문제인데, 괜히 어렵게 인접 리스트를 만들고, 중심부 엣지가 모든 엣지와 연결되어 있는지 확인하려는 절차를 거쳤다. 이렇게 하니까 효율성 검사 탈락함.