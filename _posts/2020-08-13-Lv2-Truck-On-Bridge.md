---
layout: post
title: (프로그래머스 Lv2) 다리를 지나는 트럭
subtitle: 다리를 지나는 트럭 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv2, python, deque, observe ]
category: 프로그래머스
---

<center>
  <h2>
    Lv2. 다리를 지나는 트럭 ( Python )
  </h2>
</center>

---

[Lv2. 다리를 지나는 트럭 Link](https://programmers.co.kr/learn/courses/30/lessons/42583)

### <span style="color:skyblue"># 문제 설명</span>

트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.

예를 들어, 길이가 2이고 10kg 무게를 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

| 경과 시간 | 다리를 지난 트럭 | 다리를 건너는 트럭 | 대기 트럭 |
| --------- | ---------------- | ------------------ | --------- |
| 0         | []               | []                 | [7,4,5,6] |
| 1~2       | []               | [7]                | [4,5,6]   |
| 3         | [7]              | [4]                | [5,6]     |
| 4         | [7]              | [4,5]              | [6]       |
| 5         | [7,4]            | [5]                | [6]       |
| 6~7       | [7,4,5]          | [6]                | []        |
| 8         | [7,4,5,6]        | []                 | []        |

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

### <span style="color:skyblue"># 제한 사항</span>

- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.

### <span style="color:skyblue"># 입출력 예</span>

| bridge_length | weight | truck_weights                   | return |
| ------------- | ------ | ------------------------------- | ------ |
| 2             | 10     | [7,4,5,6]                       | 8      |
| 100           | 100    | [10]                            | 101    |
| 100           | 100    | [10,10,10,10,10,10,10,10,10,10] | 110    |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **각 Time 에 따른 다리 위의 무게 상태를 체크 한다. **

>    이 문제를 풀기 위해서는 **각 초 단위의 시간 상에서 다리 위의 무게 상태를 확인**할 수 있어야 한다. 이를 위해 각 초를 기록하는 타이머와 현재 다리 위의 총 무게를 기록하는 변수를 두고, 각 **상태를 감지**하게 한다. 
>
>   ```python
>   timer, total_weight = 0, 0
>   # virtually express the bridge's current status
>   onBridge = deque([0 for _ in range(bridge_length)])
>   trucks = deque(truck_weights)
>   ```
>
>    시간을 1초씩 증가시키면서, 위에서 선언한 **onBridge 데크를 이용해 현재 다리의 상태를 Observe** 한다.
>
>   1. 만약 새로운 트럭이 다리 위에 오르더라도 다리가 충분히 무게를 견딜 수 있다면, 새로운 트럭을 다리 위에 올린다. 이 때 **total_weight 변수의 값을 갱신해줌으로서 다리 위의 총 하중을 관리**할 수 있다. 이와 같이 관측 변수를 따로 두는 이유는, <span style='color:red'>매번 onBridge 데크를 sum() 함수를 이용해 총합을 구할 경우 다리의 길이가 지나치게 길다면 배열의 O(n) 의 시간 복잡도를 가지기 때문에 시간 초과를 유발할 수 있기 때문에 이를 피하기 위함</span>이다. 
>   2. 다리가 새로운 트럭이 올랐을 때의 하중을 견딜 수 없다면, 트럭이 오르지 못했으므로 0 을 삽입하여 **단순히 다리 위의 트럭이 움직이는 것만을 표현**한다.
>
>   ```python
>   # tick the timer for 1 sec, and pass the vehicle which is on front.
>   timer += 1
>   total_weight -= onBridge.popleft()
>   # load the truck
>   if total_weight + trucks[0] <= weight:
>   		truck = trucks.popleft()
>   		onBridge.append(truck)
>   		total_weight += truck
>   # can't load the truck
>   else:
>   		onBridge.append(0)
>   ```
>
>   
>
>   이를 반복을 통해 구현하고, 남은 트럭이 없다면 종료하고 *다리의 길이를 합한 후 총 지난 시간을 반환* 하면 된다.
>
>   <br>

<br>

### 전체 코드

```python
from collections import deque

def solution(bridge_length, weight, truck_weights):
    timer, total_weight = 0, 0
    # virtually express the bridge's current status
    onBridge = deque([0 for _ in range(bridge_length)])
    trucks = deque(truck_weights)
    
    while trucks:
        # tick the timer for 1 sec, and pass the vehicle which is on front.
        timer += 1
        total_weight -= onBridge.popleft()
        # load the truck
        if total_weight + trucks[0] <= weight:
            truck = trucks.popleft()
            onBridge.append(truck)
            total_weight += truck
        # can't load the truck
        else:
            onBridge.append(0)
            
    return timer + bridge_length
```