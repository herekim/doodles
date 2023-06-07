2023-06-07
14:06

해결 여부: ✅
문제: [2574. Left and Right Sum Differences](https://leetcode.com/problems/left-and-right-sum-differences/description/)
소요시간: 12m

# 풀이 계획
1. 초기에 leftSum, rightSum 변수 만들어준다.
2. for문 돌면서 answer에 leftSum - rightSum의 절대값 넣어준다.
3. leftSum에 현재 값 추가, rightSum에 다음 값 제거해준다.
# 풀이 코드 
```javascript
var leftRightDifference = function(nums) {
    const answer = []

    let leftSum = 0
    let rightSum = nums.reduce((acc, cur, idx) => {
        if(idx !== 0) {
            return acc += cur
        }
        else {
            return 0
        }
    }, 0)

    for(let i = 0; i < nums.length; i++) {
        answer.push(Math.abs(leftSum - rightSum))

        leftSum += nums[i]
        if(nums[i+1]) {
            rightSum -= nums[i+1]
        }
    }

    return answer
};
```
# 예상 유형
- 누적합
# 시간 복잡도
ㅒ
# 새롭게 알게된 것