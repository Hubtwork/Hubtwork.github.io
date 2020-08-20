---
layout: post
title: (프로그래머스 Lv1) 문자열 내림차순으로 배치하기
subtitle: 문자열 내림차순으로 배치하기 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, sort, sorted, join]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 문자열 내림차순으로 배치하기 ( Python )
  </h2>
</center>

---

[Lv1 문자열 내림차순으로 배치하기 Link](https://programmers.co.kr/learn/courses/30/lessons/12917)

### <span style="color:skyblue"># 문제 설명</span>

문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.

### <span style="color:skyblue"># 제한 사항</span>

- str은 길이 1 이상인 문자열입니다.

### <span style="color:skyblue"># 입출력 예</span>

| s       | return  |
| ------- | ------- |
| Zbcdefg | gfedcbZ |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **문자열의 각 문자를 정렬하고 다시 문자열로 되돌리기**

>   문자열을 list 로 변환하고 나면 sort() 를 활용해 정렬할 수 있다. <u>문자의 정렬 기준은 ASCII 코드</u> 이므로 대문자가 더 작은 값을 갖기 때문에 대문자가 더 앞에 정렬되는 것을 확인할 수 있다. 
>
>   배열에 있는 요소들을 문자열로 다시 바꾸는 방법은 **join() 함수**를 활용한다. <span style='color:red'>join 함수는 앞의 character 를 각 요소간의 경계로 삼아 리스트를 문자열로 바꿔준다.</span> 리스트를 단순히 문자열로 바꾸고 싶다면 ''.join() 을, 쉼표를 매 요소 사이에 추가하고 싶다면 ','.join() 등 다양한 활용이 가능하다. 
>
>   ```python
>   s = 'AabBC'
>   print(''.join(sorted(list(s))))
>   # >> 'ABCab'
>   print(''.join(sorted(list(s), reverse=True)))
>   # >> 'baCBA'
>   print(' '.join(sorted(list(s))))
>   # >> 'A B C a b '
>   ```
>
>   <br>
>
>   문제에서 원하는 것은 문자열의 역순 정렬이므로 역순 정렬한 배열을 문자열로 바꾸어 반환해준다. 전체 코드는 아래와 같다. 

<br>

### 전체 코드

```python
def solution(s):
    return ''.join(sorted(list(s), reverse=True))
```

