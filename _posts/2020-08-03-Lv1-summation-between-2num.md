---
layout: post
title: (프로그래머스 Lv1) 두 정수 사이의 합
subtitle: 두 정수 사이의 합 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, min/max, sum, list declaration]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 두 정수 사이의 합 ( Python )
  </h2>
</center>

---

[Lv1 두 정수 사이의 합 Link](https://programmers.co.kr/learn/courses/30/lessons/12912)

### <span style="color:skyblue"># 문제 설명</span>

두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.

### <span style="color:skyblue"># 제한 사항</span>

- a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
- a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
- a와 b의 대소관계는 정해져있지 않습니다.

### <span style="color:skyblue"># 입출력 예</span>

| a    | b    | return |
| ---- | ---- | ------ |
| 3    | 5    | 12     |
| 3    | 3    | 3      |
| 5    | 3    | 12     |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **a, b 의 대소관계를 판단하고 a ~ b 까지의 수를 모두 구한다. **

>  문제에서 요구하는 것은 주어진 두 수 사이의 모든 수를 구하고, 그 합을 반환하는 것이다. 일차적으로 두 수 사이의 모든 수를 구하는 것은 <span style='color:blue'>반복을 활용한 리스트 선언</span>을 통해 쉽게 가능하다. **min()** 과 **max()** 를 활용해 두 수중 *더 작은 수 부터 높은 수 까지 반복문을 시행* 하면 이를 손쉽게 구할 수 있다.
>
>  ```python
>  # get all numbers a ~ b ( check scale relationship by min / max )
>  arr = [i for i in range(min(a,b), max(a,b)+1)]
>  ```
>
>  <br>
>
>  이 후, 우리는 단순히 **sum(Iterable)** 을 활용해 그 합을 구하고 반환해주면 된다. **sum()** 은 *주어진 이터러블에 대해 **직접 반복을 시행**해 모든 원소의 값을 더한 것을 반환* 해준다. 앞에 강조한 것과 같이 직접 반복을 시행하기 때문에 **Iterable 의 크기가 클 수록 속도가 저해** 된다는 것을 주의하자.
>
>  ```python
>  # return summation
>  return sum(arr)
>  ```
>
>  <br>
>
>  결과 코드는 다음과 같다. 

<br>

### 전체 코드

```python
def solution(a, b):
  	# get all numbers a ~ b ( check scale relationship by min / max )
    arr = [i for i in range(min(a,b), max(a,b)+1)]
    # return summation
    return sum(arr)
```

