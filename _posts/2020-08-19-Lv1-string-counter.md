---
layout: post
title: (프로그래머스 Lv1) 문자열 내 p와 y의 개수
subtitle: 문자열 내 p와 y의 개수 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, collections, counter]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 문자열 내 p와 y의 개수 ( Python )
  </h2>
</center>

---

[Lv1 문자열 내 p 와 y 의 개수 Link](https://programmers.co.kr/learn/courses/30/lessons/12916)

### <span style="color:skyblue"># 문제 설명</span>

대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

예를 들어 s가 pPoooyY면 true를 return하고 Pyy라면 false를 return합니다.

### <span style="color:skyblue"># 제한 사항</span>

- 문자열 s의 길이 : 50 이하의 자연수
- 문자열 s는 알파벳으로만 이루어져 있습니다.

### <span style="color:skyblue"># 입출력 예</span>

| s       | answer |
| ------- | ------ |
| pPoooyY | true   |
| Pyy     | false  |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **리스트 / 문자열과 같은 이터러블 내의 원소 개수를 카운트 할 수 있는 방법**

>   다른 문제 풀이에서 볼 수 있었던 *deque, defaultdict* 등 확장자료구조를 제공하는 **Python 의 내장모듈 collections**은 고맙게도, <span style='color:skyblue'>이터러블의 원소 개수를 빠르게 세고 이를 딕셔너리화 해서 저장해주는 **Counter** 를 제공</span>한다. 아래와 같이 Counter(Iterable) 을 통해 모듈을 선언하고, 이를 출력해보면 아래와 같은 결과를 확인할 수 있다.
>
>   ```python
>   from collections import Counter
>   arr = [1, 1, 4, 6, 2, 1, 3, 2, 4]
>   counter = Counter(arr)
>   # >> Counter({1: 3, 2: 2, 3: 1, 4: 2, 6: 1})
>   ```
>
>   이 문제에서는 <u>대소문자가 구분되지 않고 제공된 문자열 내에서 p 와 y 의 개수를 카운트</u> 할 수 있어야만 하므로 주어진 문자열을 먼저 **lower()** 함수를 이용해 전부 소문자로 전환 후 list 로 변환하고 Counter 모듈을 이용해 개수를 세었다. 
>
>   <BR>
>
>   ```python
>   counter = Counter(list(s.lower()))
>   ```
>
>   <br>
>
>   반환된 Counter 객체의 'p' 와 'y' 의 value 를 비교하고 그 결과를 반환하면 된다. 전체 코드는 아래와 같다. 

<br>

### 전체 코드

```python
from collections import Counter
def solution(s):
    counter = Counter(list(s.lower()))
    return True if counter['y'] == counter['p'] else False
```

