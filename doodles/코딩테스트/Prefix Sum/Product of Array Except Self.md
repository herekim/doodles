2023-06-07
15:06

해결 여부: ❌
문제: [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)
소요시간: [60m]

# 풀이 코드
```javascript
var productExceptSelf = function(nums) {
    const output = Array.from({ length : nums.length }).fill(1)

    let leftSum = 1
    for (let i = 0; i < nums.length; i++) {
        output[i] *= leftSum
        leftSum *= nums[i]
    }

    let rightSum = 1
    for (let j = nums.length - 1; j >= 0; j--) {
        output[j] *= rightSum
        rightSum *= nums[j]
    }

    return output
}
```
# 예상 유형
- 누적합
 
# 시간 복잡도
- O(n)

# 새롭게 알게된 것
- 왼쪽 값, 오른쪽 값 함께 계산하는 게 아니라 따로 계산해서 합치는 방식으로 누적합 구할 수 있다.