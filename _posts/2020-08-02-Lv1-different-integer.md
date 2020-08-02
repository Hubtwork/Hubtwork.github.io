---
layout: post
title: (프로그래머스 Lv1) 같은 숫자는 싫어
subtitle: 같은 숫자는 싫어 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, check]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 같은 숫자는 싫어 ( Python )
  </h2>
</center>


------

[Lv1 같은 숫자는 싫어 Link](https://programmers.co.kr/learn/courses/30/lessons/12906)

### <span style="color:skyblue"># 문제 설명</span>

배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다. 예를 들면,

- arr = [1, 1, 3, 3, 0, 1, 1] 이면 [1, 3, 0, 1] 을 return 합니다.
- arr = [4, 4, 4, 3, 3] 이면 [4, 3] 을 return 합니다.

배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.

### <span style="color:skyblue"># 제한 사항</span>

- 배열 arr의 크기 : 1,000,000 이하의 자연수
- 배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수

### <span style="color:skyblue"># 입출력 예</span>

| arr             | answer    |
| --------------- | --------- |
| [1,1,3,3,0,1,1] | [1,3,0,1] |
| [4,4,4,3,3]     | [4,3]     |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **연속적으로 등장하는 값을 Check 할 수 있는가 ? **

>  이 문제의 핵심은 연속적인 값을 Check 할 수 있는지다. 단순히 **어떤 숫자들이 등장했는지만 확인하는 것은 set(Iterable) 을 통해 중복값을 제거하는 것**으로 가능하다. 하지만 <span style="color:red">문제에서 원하는 것은 같은 숫자가 연속적으로 등장했을 시, 그 숫자를 하나만 보여주는 것</span>이므로 체크 변수를 통해 이를 검증하는 과정을 거쳐야 한다. 필자는 주어진 배열을 순회하면서 **체크 변수와 값이 같은지 확인 ( 연속적인 숫자인지 )** 하고 다르다면 결과 배열에 추가한 뒤 체크 배열의 값을 바꿔주는 방식을 취해 문제를 해결하였다.
>
>  ```python
>  # check continuous value by check-variable.
>  check = -1
>  # traverse all input array
>  for element in arr:
>     # if current element is different with check, it's not continuous integer. 
>   	 if element != check:
>      	# if it's new integer, append to result array and change the check.
>    	  answer.append(element)
>    	  check = element
>  ```
>
>  <br>
>
>  그 후, 완성된 결과 배열을 반환하여 준다. 결과 코드는 다음과 같다. 

<br>

### 전체 코드

```python
def solution(arr):
    answer = []
    # check continuous value by check-variable.
		check = -1
		# traverse all input array
		for element in arr:
   			# if current element is different with check, it's not continuous integer. 
 	 			if element != check:
    		# if it's new integer, append to result array and change the check.
            answer.append(element)
            check = element
    return answer
```

