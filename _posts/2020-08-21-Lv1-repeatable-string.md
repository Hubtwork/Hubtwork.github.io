---
layout: post
title: (프로그래머스 Lv1) 수박수박수박수박수박수?
subtitle: 수박수박수박수박수박수? 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, string, list comprehension, join ]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 수박수박수박수박수박수? ( Python )
  </h2>
</center>

---

[Lv1 수박수박수박수박수박수? Link](https://programmers.co.kr/learn/courses/30/lessons/12922)

### <span style="color:skyblue"># 문제 설명</span>

길이가 n이고, 수박수박수박수....와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 수박수박을 리턴하고 3이라면 수박수를 리턴하면 됩니다.

### <span style="color:skyblue"># 제한 사항</span>

- n은 길이 10,000이하인 자연수입니다.

### <span style="color:skyblue"># 입출력 예</span>

| n    | return   |
| ---- | -------- |
| 3    | 수박수   |
| 4    | 수박수박 |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **List Comprehension 을 통한 조건부 리스트를 사용할 줄 아는가 ?**

>   **Python** 에서 리스트를 선언할 때, 일정 조건을 부여하여 선언할 수 있다. 이를 List Comprehension 이라고 한다.  
>
>   1. **List with Conditional Values** : Python 에서 <span style='color:red'>반복문의 인자에 대해 각 인자의 조건을 만족하는 경우에만 </span>Value 를 삽입하여 리스트를 생성할 수 있다.
>   2. **List with Conditional Reference** : Python 에서 <span style='color:red'>반복문의 인자를 활용해 다른 Iterable 의 값을 반복적으로 참조</span>해 리스트를 생성할 수 있다. 
>
>   ```python
>   print([ i for i in range(5) if i%2==0])
>   # >> [0, 2, 4] ... List with Conditional Values
>   print(['가나다'[i%3] for i in range(5)])
>   # >> ['가','나','다','가','나','다'] ... List with Conditional Reference
>   ```
>
>   <br>
>
>   문제에서 원하는 것은 <u>두 문자 '수' 와 '박' 을 반복적으로 나타낸 길이 n 의 문자열을 반환하는 것</u> 이므로 **" '수박'  String 을 조건부 참조 "** 하여 리스트를 생성후 <u>join() 함수</u>를 활용해 결과를 반환한다. 전체 코드는 아래와 같다. 

<br>

### 전체 코드

```python
def solution(n):
    return ''.join(['수박'[i%2] for i in range(n)])
```

