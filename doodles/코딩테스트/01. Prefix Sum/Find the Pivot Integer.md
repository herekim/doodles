2023-06-07
14:06

해결 여부: ✅
문제: [2485. Find the Pivot Integer](https://leetcode.com/problems/find-the-pivot-integer/description/)
소요시간: 12m

# 풀이 계획
1. prefixSum에 1을 pivotSum에 1부터 n까지 더한 값을 미리 저장한다.
2. prefixSum, pivotSum이 같다면 prefixSum 반환한다.
3. for문을 2부터 돌면서 prefixSum에 j를 추가하고, pivotSum에 j-1을 제거하는 작업을 반복한다.
4. for문을 돌다가 prefixSum === pivotSum이 되는 순간 j를 반환한다.
5. 만약 for문을 다 돌 때까지 값이 없다면 -1을 반환한다
# 풀이 코드 
```javascript
var pivotInteger = function(n) {
    let prefixSum = 1
    let pivotSum = n * ( n + 1 ) / 2

    if(prefixSum === pivotSum) return prefixSum

    for(let j = 2; j <= n; j++) {
        prefixSum += j
        pivotSum -= j - 1

        if(prefixSum === pivotSum) {
            return j
        }
    }
    
    return -1
}
```
# 예상 유형
누적합
# 시간 복잡도
O(n)
# 새롭게 알게된 것
- 가우스의 덧셈. 1부터 n까지의 합은 n * (n + 1) / 2