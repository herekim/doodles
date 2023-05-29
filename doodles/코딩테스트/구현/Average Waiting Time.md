2023-05-29
09:05

해결 여부: ✅
문제: [LeetCode 1701. Average Waiting Time](https://leetcode.com/problems/average-waiting-time/description/)
소요시간: 35m

# 풀이 계획
1. 완료시간, 총 대기시간을 let 변수로 저장. 처음에는 완료시간을 `customers[0][0]`으로 저장
2. 조건에 따라서 완료 시간에 값 할당
	1. 고객의 도착과 주문이 밀리는 경우에는 기존 완료시간에 현재 고객 음식 준비시간 더한 값이 완료시간
	2. 현재 고객의 준비 시간이 종료되고 난 뒤에 다음 고객이 도착하는 경우에는 고객의 도착 시간과 음식 준비시간을 더한 값이 완료시간
3. 총 대기시간은 완료 시간 - 도착 시간
4. 총 대기시간을 고객 수로 나눈 값 반환

# 풀이 코드 
```js
var averageWaitingTime = function(customers) {
    let endTime = customers[0][0]
    let allWaitingTime = 0

    for(const [arrival, time] of customers) {
        endTime = arrival + time > endTime + time ? arrival + time : endTime + time
        allWaitingTime += endTime - arrival
    }

    return allWaitingTime / customers.length
};
```
# 예상 유형
구현
 
# 시간 복잡도
O(n)

# 새롭게 알게된 것
-