---
layout: post
title: (프로그래머스 Lv1) 크레인 인형 뽑기
subtitle: 크레인 인형 뽑기 문제 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, 스택, 카카오]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 크레인 인형 뽑기 ( Python )
  </h2>
</center>

------
[Lv1 크레인 인형 뽑기 link](https://programmers.co.kr/learn/courses/30/lessons/64061)
<br>
 2019 카카오 개발자 겨울 인턴쉽에서 출제되었던 문제이다. 카카오 에서 출제되는 코딩테스트 문제에는 매 번 게임에 관련한 문제가 출제된다. 다행히 본 문제는 기본적인 로직이 단순하여 다음 사항만 고려하면 풀이가 어렵지 않다.

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **게임 보드에 대한 처리 *( 선택 )***

>  게임 보드는 n * n 크기의 격자로 주어지며, 크레인이 인형을 집는 것은 각 라인의 가장 위 인형부터 집는다. 프로그래밍 상에서의 이차원 배열은 행 / 열의  순으로 구성되어 있으므로 크레인이 인형을 집는 과정을 처리할 때, 이를 쉽게 하기 위해 오른쪽으로 90도 돌렸고 이와 같이 보드를 회전시킨다면 <span style="color:red">크레인이 a 격자의 인형을 집는 것 = board[a] 의 0이 아닌 마지막 요소를 빼내는 것</span> 으로 생각할 수 있다. 
>
> ~~~python
> # Rotate 90 degrees in right direction.
> def rotate(board):
>     n = Game.size
>     arr = [deque() for _ in range(n)]
>     for i in range(n):
>         for j in range(n-1, -1, -1):
>             if board[i][j] != 0:
>                 arr[j].appendleft(board[i][j])
>     return arr
> ~~~
<br>
- **크레인이 인형을 집고 바구니에 놓을 때, 검증 및 처리**

> 크레인이 인형을 집어 바구니에 놓을 때 고려해야하는 것은 두 가지다. 
>
> 1. 크레인이 집을 라인에 인형이 있는가? **( 없다면 해당 과정은 무시 )**
> 2. 집은 인형을 바구니에 놓을 때 동일 인형이 인접해있는지 검사 및 처리 **( 동일한 인형이 인접해 있다면 제거 및 개수 카운트 )**
>
>   1번 조건의 경우, **max() 함수**를 활용해 0 보다 큰 숫자가 있는지를 판단하였다. 만약 인형이 없다면 인형을 집는 과정을 패스한다. 인형이 있다면 해당 라인의 마지막 위치에 있는 인형을 가져오고 그 자리의 값을 0 으로 설정해 비운다. 
>
>   인형을 집었다면, 현재 바구니 스택을 검증한다. **바구니가 비어있다면 단순히 인형을 집어넣는 과정을 거치고 종료**시킨다. 만약 바구니에 인형이 있다면, 바구니의 마지막 인형이 현재 집은 인형과 같은지 확인하는 검증과정을 거친다. **인형이 같으면 두 인형을 삭제해야하므로 마지막 요소를 pop() 하고 카운트를 증가**시키고 아니라면 인형을 바구니에 집어넣고 종료시킨다.
>
> ```python
> def grab(x):
>     i = Game.size-1
>     # If there's no Doll in line.
>     if max(Game.board[x-1]) == 0:
>         return
> 		# Find Last element which is not 0 = Doll
>     while True:
>         if Game.board[x-1][i] != 0:
>             break
>         i -= 1
>     # Get Doll and delete that location.
>     block = Game.board[x-1][i]
>     Game.board[x-1][i] = 0
>     # if stack is empty, just put the Doll.
>     if len(Game.stack) == 0:
>         Game.stack.append(block)
>         return
> 		# if stack's last Doll is same as Current Doll, Boom last one and add the count.
>     if Game.stack[-1] == block:
>         Game.stack.pop()
>         Game.cnt += 2
>     else:
>         Game.stack.append(block)
> ```
<br><br>
 
### 전체 코드 

```python
class Game:
    board = []
    stack = []
    cnt = 0
    size = 0

def rotate(board):
    n = Game.size
    arr = [[0 for _ in range(n)] for _ in range(n)]
    for i in range(n):
        for j in range(n-1, -1, -1):
            arr[j][n-i-1] = board[i][j]
    return arr

def grab(x):
    i = Game.size-1
    if max(Game.board[x-1]) == 0:
        return

    while True:
        if Game.board[x-1][i] != 0:
            break
        i -= 1
    block = Game.board[x-1][i]
    Game.board[x-1][i] = 0
    if len(Game.stack) == 0:
        Game.stack.append(block)
        return

    if Game.stack[-1] == block:
        Game.stack.pop()
        Game.cnt += 2
    else:
        Game.stack.append(block)

def solution(board, moves):
    Game.size = len(board)
    Game.board = rotate(board)
    for m in moves:
        grab(m)
    return (Game.cnt)
```

