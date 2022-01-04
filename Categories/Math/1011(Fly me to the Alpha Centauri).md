# 31011 (Fly me to the Alpha Centauri)

> 문제 설명

우주선 하나가 있다. 이 우주선은 이전에 k광년을 이동했을 경우 k-1, k, k+1 중에서 하나의 광년 만큼 이동이 가능합니다. 예를 들어 우주선이 이전에 1광년 만큼 이동했다면 0, 1, 2 중 하나의 광년만큼 이동할 수 있다. 이 우주선이 x지점에서 출발하여 y지점을 향해 이동하려 한다. 단, y지점에 도착하기 바로 직전의 이동거리는 반드시 1광년이어야 한다. x지점에서 y지점으로 이동하는데 필요한 이동 횟수의 최솟값을 구하는 프로그램을 작성하시오.

> 전체 코드

```node.js
const fs = require('fs')
const input = fs.readFileSync('/dev/stdin').toString().split('\n') 

const T = parseInt(input[0])
for( let i = 0; i<T; i++){
    const XY = input[i+1].split(' ')
    let X = parseInt(XY[0])  
    let Y = parseInt(XY[1])    
    
    let distance = Y-X
    let max = Math.floor(Math.sqrt(distance))
    
    // 구간1
    if(distance == max*max){
        console.log((2*max)-1)
    }
    // 구간2
    else if(distance <= max*max + max){
        console.log(2*max)
    }
    // 구간3
    else{
        console.log((2*max)+1)
    }
}
```

> 코드 설명

1. require()을 사용하여 fs모듈을 불러와서 fs 변수에 저장한다.

2. fs.readFileSync()를 사용하여 파일을 동기적으로 불러오고 toString()을 사용하여 문자열로 만들고 split('\n')을 이용하여 문자열을 한 줄 단위로 쪼개서 배열을 만들고 배열을 input 변수에 저장한다.

3. T 변수에 input 배열에 0번째 인덱스의 값을 parseInt()를 사용하여 정수형으로 변환하여 저장한다.

4. 테스트 케이스 만큼 반복한다

5. input[i+1]번째를 split(' ')를 사용하여 띄어쓰기를 기준으로 쪼개서 배열을 만들고 XY 변수에 저장한다.

6. XY의 0번째 요소를 parseInt()를 사용하여 정수형으로 변환하고 X 변수에 저장한다.

7. XY의 1번째 요소를 parseInt()를 사용하여 정수형으로 변환하고 Y 변수에 저장한다.

8. x에서 y까지의 거리를 distance에 저장한다.

   | Distance |    move     | Count | max  |
   | :------: | :---------: | :---: | :--: |
   |    1     |      1      |   1   |  1   |
   |    2     |     1 1     |   2   |  1   |
   |    3     |    1 1 1    |   3   |  1   |
   |    4     |    1 2 1    |   3   |  2   |
   |    5     |   1 2 1 1   |   4   |  2   |
   |    6     |   1 2 2 1   |   4   |  2   |
   |    7     |  1 2 2 1 1  |   5   |  2   |
   |    8     |  1 2 2 2 1  |   5   |  2   |
   |    9     |  1 2 3 2 1  |   5   |  3   |
   |    10    | 1 2 3 2 1 1 |   6   |  3   |

9. 위 표는 x부터 y까지의 거리, 우주선의 움직임, 우주선 이동 횟수, 우주선 최고 이동 거리를 나타낸다. 위에서 볼 수 있듯이 max값은 Distance 값의 제곱근이 된다. Math.sqrt()는 제곱근을 반환하고 Math.floor()은 내림한 값을 반환한다.

10. max를 제곱했을 때 Distance가 될 경우, Count는 2*max-1이 된다.

11. 구간1을 제외하고 Distance <= max*max+max 인 구간의 Count는 2 * max가 된다.

12. 구간1과 구간2를 모두 제외한 구간3의 Count는 2*max+1이 된다.



