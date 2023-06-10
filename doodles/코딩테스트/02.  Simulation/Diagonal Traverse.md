2023-05-31
10:05

해결 여부: ✅
문제: [498. Diagonal Traverse](https://leetcode.com/problems/diagonal-traverse/)
소요시간: 55m

# 풀이 계획
1. while문을 돌면서 result의 길이가 mat[0].length x mat.length 보다 작을 때까지 반복
2. 오른쪽 상단, 왼쪽 하단 방향을 가진 플래그 변수 생성
3. 행, 열 위치를 파악하는 로케이션 변수 생성
4. 반환할 result 배열 생성
5. while문을 돌면서 mat 매트릭스에 현재 위치를 result에 push
6. 플래그가 오른쪽 상단이면서 다음 인덱스에 요소가 있을 경우 location을 오른쪽 상단으로 이동
7. 플래그가 오른쪽 상단이면서 다음 인덱스에 요소가 없을 경우
	1. 플래그 변수를 바꿈
	2. 오른쪽 요소가 있을 경우 location을 오른쪽으로 이동하고
	3. 없을 경우 location을 아래쪽으로 이동
8. 플래그가 왼쪽 하단이면서 다음 인덱스에 요소가 있을 경우 location을 왼쪽 하단으로 이동
9. 플래그가 왼쪽 하단이면서 다음 인덱스에 요소가 없을 경우 
	1. 플래그 변수를 바꿈
	2. 하단에 요소가 있을 경우 location을 하단으로 이동
	3. 없을 경우 location을 오른쪽으로 이동
# 풀이 코드 
```javascript
var findDiagonalOrder = function(mat) {
    let flag = 'rightAndUp' // 'leftAndDown'
    let location = [0,0] // [행위치, 열위치]
    let result = []

    while(result.length < mat[0].length * mat.length) {
        result.push(mat[location[0]][location[1]])

        if(flag === 'rightAndUp') {
            if(mat[location[0]-1] !== undefined 
            && mat[location[0]-1][location[1]+1] !== undefined) {
                location[0]--
                location[1]++
            }
            else {
                flag = 'leftAndDown'
                if(mat[location[0]] !== undefined 
                && mat[location[0]][location[1]+1] !== undefined) {
                    location[1]++
                }
                else {
                    location[0]++
                }
            }
            continue
        }

        if(flag === 'leftAndDown') {
            if(mat[location[0]+1] !== undefined 
            && mat[location[0]+1][location[1]-1] !== undefined) {
                location[0]++
                location[1]--
            }
            else {
                flag = 'rightAndUp'
                if(mat[location[0]+1] !== undefined 
                && mat[location[0]+1][location[1]] !== undefined) {
                    location[0]++
                }
                else {
                    location[1]++
                }
            }
            continue
        }
    }
    return result;
};
```
# 예상 유형
구현
 
# 시간 복잡도
O(n)

# 새롭게 알게된 것
- 행, 열 위치를 배열로 표기하고 이를 바꾸면서 이동하는 것을 여러 곳에서 활용할 수 있겠다