---
layout: post
title: (프로그래머스 Lv1) 문자열 내 마음대로 정렬하기
subtitle: 문자열 내 마음대로 정렬하기 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, sort, key, lambda, multiple key]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 문자열 내 마음대로 정렬하기 ( Python )
  </h2>
</center>

---

[Lv1 문자열 내 마음대로 정렬하기 Link](https://programmers.co.kr/learn/courses/30/lessons/12915)

### <span style="color:skyblue"># 문제 설명</span>

문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 예를 들어 strings가 [sun, bed, car]이고 n이 1이면 각 단어의 인덱스 1의 문자 u, e, a로 strings를 정렬합니다.

### <span style="color:skyblue"># 제한 사항</span>

- strings는 길이 1 이상, 50이하인 배열입니다.
- strings의 원소는 소문자 알파벳으로 이루어져 있습니다.
- strings의 원소는 길이 1 이상, 100이하인 문자열입니다.
- 모든 strings의 원소의 길이는 n보다 큽니다.
- 인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.

### <span style="color:skyblue"># 입출력 예</span>

| strings           | n    | return            |
| ----------------- | ---- | ----------------- |
| [sun, bed, car]   | 1    | [car, bed, sun]   |
| [abce, abcd, cdx] | 2    | [abcd, abce, cdx] |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **다중 키를 활용한 리스트 요소 정렬 **

>   주어진 정수 n 의 인덱스 글자에 대해 주어진 리스트를 정렬하는 것이 문제의 목적이다. **Python 에서는 리스트와 같은 Iterable 을 정렬하여 반환**해주는 **sorted()** 함수를 활용할 수 있다. 이 때 key 를 주어주지 않으면 이를 사전순 혹은 수의 크기 기준 정렬을 하지만, <span style='color:skyblue'>**key 를 적용 **하면 우리가 원하는 key 에 따른 정렬 결과</span>를 얻을 수 있다. 물론 Python 의 내장 sort 는 가장 높은 효율성을 보장한다.
>
>   key 의 적용에 따른 차이는 아래와 같다. 
>
>   1. **기본 Sort** : 0번 인덱스 기준 정렬, 0번 인덱스가 동일할 시 1번, 1번 인덱스가 동일할 시 2번 기준 정렬...
>   2. **Sort with key = x[1]** : 1번 인덱스 기준 정렬, <u>1번 인덱스가 동일할 시 기존 리스트의 순서</u>에 따라 정렬
>   3. **Sort with key = (x[1], x)** : 1번 인덱스 기준 정렬, <u>1번 인덱스가 동일할 시 사전순</u> 정렬 *( key = x 적용 )*
>
>   <BR>
>
>   ```python
>   Iterable = ['bbd', 'abc', 'bad']
>   sorted(Iterable)
>   # >> ['abc','bad','bbd']
>   sorted(Iterable, key=lambda x:x[1])
>   # >> ['bad', 'bbd', 'abc']
>   sorted(Iterable, key=lambda x:(x[1], x))
>   # >> ['bad', 'abc', 'bbd']
>   ```
>
>   <br>
>
>   문제에서는 n 번 인덱스 기준 정렬 후 만약 n번 인덱스가 같다면 사전 정렬을 하여야 하기 때문에 복합 키인 **key = (x[n], x) **를 사용하여 구현한다. 전체 코드는 아래와 같다.

<br>

### 전체 코드

```python
def solution(strings, n):
    return sorted(strings, key=lambda x:(x[n], x))
```

