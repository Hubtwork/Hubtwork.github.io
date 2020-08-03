---
layout: post
title: (프로그래머스 Lv1) 나누어 떨어지는 숫자 배열
subtitle: 나누어 떨어지는 숫자 배열 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, modular, even/odd, conditional list]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 나누어 떨어지는 숫자 배열 ( Python )
  </h2>
</center>

---

[Lv1 나누어 떨어지는 숫자 배열 Link](https://programmers.co.kr/learn/courses/30/lessons/12910)

### <span style="color:skyblue"># 문제 설명</span>

array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.
divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 -1을 담아 반환하세요.

### <span style="color:skyblue"># 제한 사항</span>

- arr은 자연수를 담은 배열입니다.
- 정수 i, j에 대해 i ≠ j 이면 arr[i] ≠ arr[j] 입니다.
- divisor는 자연수입니다.
- array는 길이 1 이상인 배열입니다.

### <span style="color:skyblue"># 입출력 예</span>

| arr           | divisor | return        |
| ------------- | ------- | ------------- |
| [5, 9, 7, 10] | 5       | [5, 10]       |
| [2, 36, 1, 3] | 1       | [1, 2, 3, 36] |
| [3,2,6]       | 10      | [-1]          |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **mod 연산을 활용하여 나누어 떨어지는 수를 판별할 수 있는가 ? **

>  문제에서 요구하는 것은 **mod 연산 ( modular arithmetic. 나머지 연산 )** 을 활용해 나누어 떨어짐을 확인할 수 있는가이다. **mod 연산자 ( % ) 를 활용해 연산을 수행하면 그 나머지를 반환**한다. 아래와 같이 좌항을 우항으로 나누었을 때의 나머지를 반환하기 때문에 이를 활용하면, <span style='color:red'>나머지연산 뿐만 아니라 짝 / 홀수 판단 등</span>을 쉽게 구현할 수 있다.
>
>  ```python
>  # modular Arithmetic example.
>  15 % 2 # >> 1
>  14 % 7 # >> 0
>  # odd / even number
>  if num % 2 == 0 : # check even number ... even number is like 2n
>  elif num % 2 == 1 : # check odd number ... odd number is like 2n-1
>  ```
>
>  <br>
>
>  이제 모듈러 연산의 용도 및 활용법을 알았으니, 이를 이용해 ***주어진 배열을 순회하며 나누어 떨어지는 수 인지를 확인하고 정답 배열에 append*** 시킨다. 이후 정답 배열을 sorted(Iterable) 을 사용해 제한사항에 맞게 오름차순으로 정렬해 반환해주고 만약 배열이 비어있다면 ( 조건을 만족하는 원소가 없다면 ) [-1] 을 반환해주면 된다. 
>
>  ```python
>  # traverse all input array
>  for num in arr:
>   		# if num is perfectly divisable by divisor, append it to answer array. 
>  		if num % divisor == 0:
>      		answer.append(num)
>  ```
>
>  필자는 이를 **조건부 리스트**를 활용해 다음과 같이 구현하였다. 리스트 생성구문에 if 문을 활용한다면 <span style='color:skyblue'><i>기존의 리스트를 순회하면서 아래와 같이 원하는 조건에 맞는 원소만 가진 리스트</i></span>를 만들 수 있다. 
>
>  ```python
>  # answer is list made by appending element which is divisable by divisor of input array
>  answer = [num for num in arr if num%divisor == 0]
>  ```
>
>  결과 코드는 다음과 같다. 

<br>

### 전체 코드

```python
def solution(arr, divisor):
  	# answer is list made by appending element which is divisable by divisor of input array
    answer = [num for num in arr if num%divisor == 0]
    # if answer list is not empty, return sorted one. else, return [-1]
    return sorted(answer) if len(answer) > 0 else [-1]
```

