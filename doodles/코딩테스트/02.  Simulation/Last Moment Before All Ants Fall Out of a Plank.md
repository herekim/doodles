2023-06-01
09:06

해결 여부: ❌
문제: [1503. Last Moment Before All Ants Fall Out of a Plank](https://leetcode.com/problems/last-moment-before-all-ants-fall-out-of-a-plank/description/)
소요시간: 40m

# 풀이 계획
1. 개미의 방향을 바꾸는 게 사실 함정인 문제
2. 왼쪽 방향, 오른쪽 방향 중 가장 멀리있는 개미가 결국 걸리는 시간이다
# 풀이 코드 
```javascript
var getLastMoment = function(n, left, right) {
    let maxLeft = left.length ? Math.max(...left) : 0
    let maxRight = right.length ? n - Math.min(...right) : 0
    
    return Math.max(maxLeft, maxRight)
};
```
# 예상 유형
구현
# 시간 복잡도
O(n)
# 새롭게 알게된 것
- 조건이 너무 복잡해지면 빠르게 이 풀이 방법이 잘못 되었을수도 있단 걸 생각해야함