2023-05-27
15:05

해결 여부: ✅
문제: [LeetCode 2679. Sum in a Matrix](https://leetcode.com/problems/sum-in-a-matrix/)
소요시간: 16m

# 풀이 계획
1. while문으로 nums[0] 배열이 비어있을 때까지 반복한다.
2. while문 내부에서 nums 배열의 for문을 돌면서 Math.max 메서드를 사용해 각 행의 최대값을 구하고, 해당 값을 splice로 삭제한다.
3. while문 바깥에서 result 변수를 만들고, while문을 돌 때 마다 max값을 더해준다.
# 풀이 코드 
```js
/**
 * @param {number[][]} nums
 * @return {number}
 */
var matrixSum = function(nums) {
    let result = 0

    while(nums[0].length > 0) {
      let max = 0

      for(const num of nums) {
        const maxOfRows = Math.max(...num)
        if(maxOfRows > max) {
          max = maxOfRows
        }
        const index = num.indexOf(maxOfRows)
        num.splice(index, 1)
      }

      result += max
    }
  return result
};
```
# 예상 유형
구현
 
# 시간 복잡도
O(n)

# 새롭게 알게된 것
-