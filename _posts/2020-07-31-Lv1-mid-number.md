---
layout: post
title: (프로그래머스 Lv1) 가운데 글자 가져오기
subtitle: 가운데 글자 가져오기 문제 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, calendar]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 가운데 글자 가져오기 ( Python )
  </h2>
</center>


------

[Lv1 가운데 글자 가져오기 Link](https://programmers.co.kr/learn/courses/30/lessons/12903)

### <span style="color:skyblue"># 문제 설명</span>

단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.

### <span style="color:skyblue"># 제한 사항</span>

- s는 길이가 1 이상, 100이하인 스트링입니다.

### <span style="color:skyblue"># 입출력 예</span>

| s     | return |
| ----- | ------ |
| abcde | c      |
| qwer  | we     |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **리스트 슬라이싱에 대한 개념적 이해가 필요하다. **

>  리스트 슬라이싱 ( List Slicing ) 이란 주어진 배열을 원하는 인덱스에 맞추어 잘라내는 과정을 말한다. python 에서는 문자열 슬라이싱 또한 리스트 슬라이싱과 같은 방식으로 이루어지기 때문에 이를 잘 숙지하고 있다면 문자열을 다뤄야하는 다양한 문제에서 이점을 가질 수 있다. 
>
>  ```python
>  arr = [1, 2, 3, 4, 5]
>  # list slicing example [ start index : end index + 1 ] 
>  arr1 = arr[2:4]
>  # >> arr1 : [3, 4]
>  s = "legend"
>  # string slicing example [ start index : end index + 1 ]
>  s1 = s[1:4]
>  # >> s1 : "ege"
>  ```
>  <br>
>  리스트 슬라이싱을 활용, 제한사항인 **단어의 길이가 홀수일 경우 중간 1글자, 단어의 길이가 짝수일 경우 중간 2글자를 반환** 을 분기문으로 처리해주면 된다.
>
>  ```python
>  # check either number is even or not. ( it can be accomplished by modular computation )
>  if len(s)%2 == 0 :
>  	answer = s[len(s)//2-1:len(s)//2+1] 
>  else:
>    answer = s[len(s)//2]
>  ```
>
>  필자는 삼항 연산의 연습을 위해 아래와 같이 구현하였다.

<br>

### 전체 코드

```python
def solution(s):
  	# check either number is even or not. ( it can be accomplished by modular computation )
    return s[len(s)//2-1:len(s)//2+1] if len(s)%2 == 0 else s[len(s)//2]
```

