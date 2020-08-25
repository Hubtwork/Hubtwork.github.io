---
layout: post
title: (프로그래머스 Lv1) [카카오 인턴] 키패드 누르기
subtitle: [카카오 인턴] 키패드 누르기 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, kakao, list, conditional flow, boolean ]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. [카카오 인턴] 키패드 누르기 ( Python )
  </h2>
</center>

---

[Lv1 \[카카오 인턴\] 키패드 누르기 Link](https://programmers.co.kr/learn/courses/30/lessons/67256)

### <span style="color:skyblue"># 문제 설명</span>


스마트폰 전화 키패드의 각 칸에 다음과 같이 숫자들이 적혀 있습니다.

![kakao_phone1.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4b69a271-5f4a-4bf4-9ebf-6ebed5a02d8d/kakao_phone1.png)

이 전화 키패드에서 왼손과 오른손의 엄지손가락만을 이용해서 숫자만을 입력하려고 합니다.
맨 처음 왼손 엄지손가락은 `*` 키패드에 오른손 엄지손가락은 `#` 키패드 위치에서 시작하며, 엄지손가락을 사용하는 규칙은 다음과 같습니다.

1. 엄지손가락은 상하좌우 4가지 방향으로만 이동할 수 있으며 키패드 이동 한 칸은 거리로 1에 해당합니다.
2. 왼쪽 열의 3개의 숫자 `1`, `4`, `7`을 입력할 때는 왼손 엄지손가락을 사용합니다.
3. 오른쪽 열의 3개의 숫자 `3`, `6`, `9`를 입력할 때는 오른손 엄지손가락을 사용합니다.
4. 가운데 열의 4개의 숫자 `2`, `5`, `8`, `0`을 입력할 때는 두 엄지손가락의 현재 키패드의 위치에서 더 가까운 엄지손가락을 사용합니다.
   4-1. 만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용합니다.

순서대로 누를 번호가 담긴 배열 numbers, 왼손잡이인지 오른손잡이인 지를 나타내는 문자열 hand가 매개변수로 주어질 때, 각 번호를 누른 엄지손가락이 왼손인 지 오른손인 지를 나타내는 연속된 문자열 형태로 return 하도록 solution 함수를 완성해주세요.

### <span style="color:skyblue"># 제한 사항</span>

- numbers 배열의 크기는 1 이상 1,000 이하입니다.
- numbers 배열 원소의 값은 0 이상 9 이하인 정수입니다.
- hand는 `"left"` 또는 `"right"` 입니다.
  - `"left"`는 왼손잡이, `"right"`는 오른손잡이를 의미합니다.
- 왼손 엄지손가락을 사용한 경우는 `L`, 오른손 엄지손가락을 사용한 경우는 `R`을 순서대로 이어붙여 문자열 형태로 return 해주세요.

### <span style="color:skyblue"># 입출력 예</span>

| numbers                           | hand      | result          |
| --------------------------------- | --------- | --------------- |
| [1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5] | `"right"` | `"LRLLLRLLRRL"` |
| [7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2] | `"left"`  | `"LRLLRRLLLRR"` |
| [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]    | `"right"` | `"LLRLLRLLRL"`  |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **입력된 수의 위치를 표현할 줄 아는가 ?**

>   문제의 요구사항을 분석해보면 <span style='color:red'>키패드는 위치에 따라 총 3가지로 표현</span>할 수 있다. 이에 각 키패드를 위치에 따라 구분지어 리스트를 구성하고 **현재 각 손이 누르고 있는 키패드의 위치 정보를 담고 있는 left, right 리스트를 선언**하였다. 다음 요구사항에 따라 계산을 하기 위해 <span style='color:skyblue'>현재 중앙에 손이 위치해있는지의 여부를 True / False 로 표현</span>하여 함께 저장한다.
>
>   **요구사항**
>
>   - 중앙에 있는 키패드를 누를 경우, <u>해당 키패드에서 가장 가까이 위치한 손</u>으로 누른다
>   - 만약 거리가 같을 시, <u>주어진 주 사용 손에 따라 해당 손</u>으로 누른다. 
>
>   ```python
>   answer = ''
>   left, right = [3, False], [3, False]
>   key_left, key_center, key_right = [1, 4, 7], [2, 5, 8, 0], [3, 6, 9]
>   ```
>
>   <br>

- **주어진 숫자에 따라 어떤 손으로 누를지 올바르게 판단할 수 있는가?**

> 미리 나눠놓은 키패드의 위치에 따른 리스트를 이용해 주어진 숫자의 배열에 따라 우선 분기를 통해 어떤 손으로 누를지 판단한다.
>
> ```python
> for n in numbers:
>   	# if given number is in left side		
>     if n in key_left:
>     # if given number is in right side		
>     elif n in key_right:
>     # if given number is in center		
>     else:
> ```
>
> <br>주어진 숫자가 왼쪽 라인에 위치한 경우와 오른쪽 라인에 위치한 경우에는 각 손으로만 누르므로 누른 후의 위치정보로 갱신해주고, *중앙에 있는 키패드를 누르지 않았으므로 2번째 값은 False 로 초기화* 한다.
>
> ```python
> if n in key_left:
>   	left = [key_left.index(n), False]
>  		answer += 'L'
> elif n in key_right:
>   	right = [key_right.index(n), False]
>     answer += 'R'
> ```
>
> <br>
>
> 주어진 숫자가 중앙에 위치한 경우 눌러야할 키패드와 각 손의 현재 위치에 따른 거리를 계산한 후 다음 두 가지 경우에 따라 어떤 손으로 누를지 산출한다.
>
> **손 선택 분기**
>
> - 거리가 같을 경우 : 현재 어떤 손이 주 손인지에 따라서 누를 손을 선택한다.
> - 거리가 다를 경우 : 거리가 더 가까이 위치해 있는 손으로 누른다.
>
> ```python
> def calc(left, right, target, hand):
>     l = abs(target - left[0]) if left[1] else abs(target - left[0])+1
>     r = abs(target - right[0]) if right[1] else abs(target - right[0])+1
>     
>     if l == r:
>         return 'L' if hand == 'left' else 'R'
>     else:
>         return 'L' if l < r else 'R'
> ```
>
> <br>
>
> 모든 숫자에 대해 어떤 손으로 눌렀는지를 문자열에 담고 이를 반환해준다. 전체 코드는 아래와 같다.

<br>

### 전체 코드

```python
def calc(left, right, target, hand):
    l = abs(target - left[0]) if left[1] else abs(target - left[0])+1
    r = abs(target - right[0]) if right[1] else abs(target - right[0])+1
    
    if l == r:
        return 'L' if hand == 'left' else 'R'
    else:
        return 'L' if l < r else 'R'

def solution(numbers, hand):
    answer = ''
    left, right = [3, False], [3, False]
    key_left, key_center, key_right = [1, 4, 7], [2, 5, 8, 0], [3, 6, 9]
    for n in numbers:
        if n in key_left:
            left = [key_left.index(n), False]
            answer += 'L'
        elif n in key_right:
            right = [key_right.index(n), False]
            answer += 'R'
        else:
            target = key_center.index(n)
            curr = calc(left, right, target, hand)
            if curr == 'L':
                left = [target, True]
                answer += 'L'
            else:
                right = [target, True]
                answer += 'R'
            
    return answer
```

