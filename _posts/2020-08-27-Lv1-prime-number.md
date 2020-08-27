---
layout: post
title: (프로그래머스 Lv1) 소수 찾기
subtitle: 소수 찾기 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, eratostenes, prime number, set]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 소수 찾기 ( Python )
  </h2>
</center>

---

[Lv1 소수 찾기 Link](https://programmers.co.kr/learn/courses/30/lessons/12921)

### <span style="color:skyblue"># 문제 설명</span>

1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.

소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.
(1은 소수가 아닙니다.)

### <span style="color:skyblue"># 제한 사항</span>

- n은 2이상 1000000이하의 자연수입니다.

### <span style="color:skyblue"># 입출력 예</span>

| n    | result |
| ---- | ------ |
| 10   | 4      |
| 5    | 3      |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **효율성 테스트를 통과할 소수 찾기 방법 **

>   단순히 주어진 숫자 이하의 소수의 개수를 찾는 것은 쉽다.
>
>   1. 2 부터 시작해 N 까지의 모든 숫자를 순회하며 해당 숫자의 약수가 존재하는지 확인한다.
>      1. 만약 존재한다면 해당 수를 카운트한다. 
>   2. 이후 소수가 아닌 수들의 개수를 뺀 숫자를 반환하면 된다. 
>
>   ```python
>   non_prime_count = 0
>   for i in range(2, n+1):
>     for j in range(2, i):
>       if i%j == 0:
>         non_prime_count += 1
>         break
>   return n - non_prime_count
>   ```
>
>   하지만 이를 응용하여 <span style='color:red'>프로그램을 구현해야할 때는 해당 알고리즘은 너무 Greedy 하여 효율성 면에서 너무 큰 단점</span>으로 작용한다. 
>   $$
>   최악시간복잡도 : O(n^2)
>   $$
>   <br>이를 위해 본 풀이에서는 **'에라토스테네스의 체'** 라는 <u>소수 판별 알고리즘</u> 을 소개한다. 고대 그리스의 수학자 에라토스테네스가 제안한 이 방식은 <span style='color:skyblue'>2부터 모든 수를 나열한 후 순서대로 지워지지않은 i 에 대해 범위 내의 i 의 배수를 모두 지운다.</span> 이를 반복해 모든 배수들을 지워나가면, 결과적으로 소수가 아닌 수 들만이 남을 것이다. 구글에서 제시하는 python 코드는 아래와 같다.
>
>   ```python
>   def prime_list(n):
>       # 에라토스테네스의 체 초기화: n개 요소에 True 설정(소수로 간주)
>       sieve = [True] * n
>   
>       # n의 최대 약수가 sqrt(n) 이하이므로 i=sqrt(n)까지 검사
>       m = int(n ** 0.5)
>       for i in range(2, m + 1):
>           if sieve[i] == True:           # i가 소수인 경우
>               for j in range(i+i, n, i): # i이후 i의 배수들을 False 판정
>                   sieve[j] = False
>   
>       # 소수 목록 산출
>       return [i for i in range(2, n) if sieve[i] == True]
>   ```
>
>   필자는 이를 python 의 set 과 range 함수 및 차집합 연산을 활용해 아래와 같이 구현했다. 
>
>   ```python
>   # Ver 2. using set
>   numbers = set(range(2, n+1))
>   for i in range(n+1):
>     if i in numbers:
>       numbers -= set(range(2*i, n+1, i))
>   ```
>
>   <br>
>
>   전체 코드는 아래와 같다.

<br>

### 전체 코드

```python
def solution(n):
    numbers = set(range(2, n+1))
    for i in range(n+1):
        if i in numbers:
            numbers -= set(range(2*i, n+1, i))
    return len(numbers)
```

