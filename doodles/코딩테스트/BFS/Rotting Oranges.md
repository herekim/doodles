2023-06-02
09:06

해결 여부: ✅
문제: [LeetCode 994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/description/)
소요시간: 30m

# 풀이 계획
1. BFS로 푸는 문제.
2. 큐에 썩은 오렌지의 x,y 좌표를 처음에 넣어준다. 그리고 신선한 오렌지의 개수 저장해준다.
3. while문을 돌면서 큐가 0보다 클 때 조건문 실행한다.
4. 썩은 오랜지 개수만큼 for문을 돌면서 썩은 오렌지를 큐에서 shift 해온다.
5. 해당 썩은 오랜지의 4방향을 for문 돌면서 신선한 오렌지가 있을 때 큐에 넣어주고, grid를 바꿔주고, 신선한 오렌지의 개수를 -1해준다.
6. while문 한번 도는 게 1분 지났다는 의미니까 while문 끝날 때 minutes++
# 풀이 코드 
```javascript
var orangesRotting = function(grid) {
    let freshOranges = 0
    let queue = []
    let minutes = -1

    for(let i = 0; i < grid.length; i++){
        for(let j = 0; j < grid[i].length; j++){
            if(grid[i][j] === 1){
                freshOranges++
            }
            if(grid[i][j] === 2){
                queue.push([i,j])
            }
        }
    }

    if(freshOranges === 0) return 0

    const directionX = [1, -1, 0, 0]
    const directionY = [0, 0, -1, 1]

    while(queue.length > 0){
        const size = queue.length

        for(let i = 0; i < size; i++){
            const [ rottenX, rottenY ] = queue.shift()

            for(let j = 0; j < 4; j++){
                const [nextX, nextY] = [ rottenX + directionX[j], rottenY + directionY[j] ]

                if(
                    nextX < 0 || 
                    nextY < 0 || 
                    nextX >= grid.length || 
                    nextY >= grid[0].length || 
                    grid[nextX][nextY] === 0 || 
                    grid[nextX][nextY] === 2
                ) continue

                queue.push([nextX,nextY])
                grid[nextX][nextY] = 2
                freshOranges--
            }
        }

        minutes++
    }

    return freshOranges === 0 ? minutes : -1
}
```
# 예상 유형
BFS
# 시간 복잡도
O(n)
# 새롭게 알게된 것
-