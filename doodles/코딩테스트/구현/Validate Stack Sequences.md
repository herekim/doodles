2023-06-03
09:06

해결 여부: ✅
문제: [LeetCode - 946. Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/description/)
소요시간: 25m

# 풀이 계획
1. 빈 스택을 만들고 이에 대한 푸시와 팝을 진행한다.
2. while문을 돌면서 푸시와 팝의 길이가 0이 아닐 때 내부를 실행한다.
3. 만약 스택의 끝과 팝의 처음이 같다면 팝에서 shift, 스택에서 pop해준다
4. 만약 스택의 끝과 팝의 처음이 같지 않다면 푸시의 처음을 shift, 스택에 push해준다  
5. 만약 푸시가 비어있고 팝이 남아있는데, 스택의 끝과 팝의 처음이 같지 않다면 false

# 풀이 코드 1
```javascript
var validateStackSequences = function(pushed, popped) {
    const stack = []

    while(pushed.length > 0 || popped.length > 0) {
        if(popped[0] === stack[stack.length - 1]) {
            popped.shift()
            stack.pop()
            continue
        }

        if(pushed.length === 0 && popped[0] !== stack[stack.length - 1]) {
            return false
        }

        stack.push(pushed.shift())
    }

    return true
};
```
# 풀이 코드2
```javascript
var validateStackSequences = function(pushed, popped) {
    const stack = []
    let pushedIndex = 0
    let poppedIndex = 0

    while(pushedIndex < pushed.length || poppedIndex < popped.length) {
        if(popped[poppedIndex] === stack[stack.length - 1]) {
            stack.pop()
            poppedIndex++
            continue
        }

        if(pushedIndex === pushed.length && popped[poppedIndex] !== stack[stack.length - 1]) {
            return false
        }


        stack.push(pushed[pushedIndex])
        pushedIndex++

    }

    return true
};
```
# 예상 유형
구현
# 시간 복잡도
풀이1 - O(n^2)
풀이2 - O(n)
# 새롭게 알게된 것
- 새롭게 알게된 것이라기 보단 첫번째 풀이는 pushed, popped도 친절하게 shift를 하나 하나 해줬지만, 이걸 index로 표현하니까 시간복잡도가 확 올라갔다(52.99% -> 72.10%)