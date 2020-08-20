---
layout: post
title: (프로그래머스 Lv1) 문자열 다루기 기본
subtitle: 문자열 다루기 기본 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, string, isalpha, isdigit, isalnum]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 문자열 다루기 기본 ( Python )
  </h2>
</center>

---

[Lv1 문자열 다루기 기본 Link](https://programmers.co.kr/learn/courses/30/lessons/12918)

### <span style="color:skyblue"># 문제 설명</span>

문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 a234이면 False를 리턴하고 1234라면 True를 리턴하면 됩니다.

### <span style="color:skyblue"># 제한 사항</span>

- `s`는 길이 1 이상, 길이 8 이하인 문자열입니다.

### <span style="color:skyblue"># 입출력 예</span>

| s    | return |
| ---- | ------ |
| a234 | false  |
| 1234 | true   |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **문자열의 숫자여부 판단 및 길이 확인**

>   **Python 의 문자열 체크 함수** 중에는 isalpha() 와 isdigit(), isalnum() 이 있다.
>
>   1. **isalpha()** : <span style='color:red'>문자열이 순수한 문자 ( 알파벳, 한글 등 )</span> 로만 이루어져있는지 여부
>   2. **isdigit()** : <span style='color:red'>숫자</span>로만 이루어져있는지 여부
>   3. **isalnum()** : <span style='color:red'>문자 + 숫자 ( 특수문자 제외 )</span> 로만 이루어져있는지 여부
>
>   ```python
>   print('abc'.isalpha(), 'a1b2'.isalpha())
>   # >> True False
>   print('a1b2'.isdigit(), '4123'.isalpha())
>   # >> False True
>   print('a1b2'.isalnum(), '#a1b2'.isalnum())
>   # >> True False
>   ```
>
>   <br>
>
>   문제에서 원하는 것은 <u>주어진 문자열이 숫자이며 길이가 4 또는 6인지 판단하는 것</u> 이므로 **" in 리스트 "** 를 활용해 길이 여부까지 확인하여 결과를 반환한다. 전체 코드는 아래와 같다. 

<br>

### 전체 코드

```python
def solution(s):
    return s.isdigit() and len(s) in [4, 6]
```

