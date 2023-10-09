# Depth First Search 깊이 우선 탐색

> [DFS-알고리즘](https://velog.io/@jiwonyyy/DFS-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
- DFS 알고리즘은 **시작점에서 출발해 가능한 멀리까지 간 후**에 다시 돌아와서 다른 방향을 탐험하는 방식
- 모든 노드를 방문하고자 하는 경우에 사용한다.
- 트리나 그래프와 같은 비선형 자료구조에서 많이 사용된다.

<br/>
  
- Stack 자료구조를 이용한 구현 방법
  
```javascript
function dfsUsingStack(graph, start) {
    const stack = [start]; // 시작 노드를 스택에 넣음
    const visited = []; // 방문한 노드를 기록하기 위한 Array

    while (stack.length > 0) {
        const current = stack.pop();

        if (!visited.includes(current)) {
            visited.push(current);
            console.log(current);

            graph[current].forEach(neighbor => {
                if (!visited.includes(neighbor)) {
                    stack.push(neighbor);
                }
            });
        }
    }
}

const graph = {
    A: ['B', 'C'],
    B: ['D', 'E'],
    C: ['F'],
    D: [],
    E: ['F'],
    F: []
};

dfsUsingStack(graph, 'A'); // 시작 노드 'A'에서 DFS 시작
```

<br/>

- 재귀를 이용한 구현 방법
  
```javascript
function dfsUsingRecursion(graph, current, visited) {
    visited.push(current);
    console.log(current);

    graph[current].forEach(neighbor => {
        if (!visited.includes(neighbor)) {
            dfsUsingRecursion(graph, neighbor, visited);
        }
    });
}

const graph = {
    A: ['B', 'C'],
    B: ['D', 'E'],
    C: ['F'],
    D: [],
    E: ['F'],
    F: []
};

const visited = [];
dfsUsingRecursion(graph, 'A', visited); // 시작 노드 'A'에서 DFS 시작
```
