문제: [2018 KAKAO BLIND RECRUITMENT](https://school.programmers.co.kr/learn/courses/30/lessons/17687)  
소요시간: 55분

# 풀이 계획
1. 전체 인원이 돌기 위해선 t*m 까지의 숫자에 대한 n진수로의 변환이 필요하다. (최적화 필요)
2. 해당 숫자까지 돌면서 새로운 배열에 해당 진수에 대한 한 자리씩 끊은 숫자를 넣는다. (이때 11진수부터는 10-15의 수를 A-F로 변환해서 넣는다.)
3. 튜브의 차례는 p에 m을 차례로 더한 값이고, 이를 t번 반복하면 된다.
4. 현재 순서가 자신의 순서라면 정답 문자열에 넣는다.

# 수도 코드
1. for문을 돌면서 t*m까지 n진수로 변환
2. 변환된 n진수를 새로운 배열에 한 자리씩 끊어서 삽입
3. 만들어진 배열을 돌면서 현재 위치를 m에서 나눴을 때 나머지가 p와 같다면 정답 문자열에 삽입

# 풀이 코드
```js
function solution(n, t, m, p) {
    let answer = '';
    let newArray = [];

    for(let i = 0; i < t*m; i++) {
        const nBaseArray = i.toString(n).split('');
        for(const splitedNBase of nBaseArray) {
            if(typeof splitedNBase === 'string') {
                newArray.push(splitedNBase.toUpperCase());
            } else {
                newArray.push(splitedNBase);   
            }
        }
    }

    for(let j = 0; j < newArray.length; j++) {
        if((j+1)%m === (p % m === 0 ? 0 : p % m)) {
            answer += newArray[j].toString();
        }
    }

    return answer.substr(0,t);
}
```
# 예상 유형
- 구현
# 시간 복잡도
- O(n log n)
# 새롭게 알게된 것
1. 현재 순서가 자신의 순서인지 알기 위해선 현재 순서를 전체 인원수로 나눈 나머지가 자신의 순서와 같아야 한다.
2. `substr` 의 첫 번째 인자로 시작 인덱스, 두 번째 인자로 길이를 지정해서 문자열을 분리할 수 있다.