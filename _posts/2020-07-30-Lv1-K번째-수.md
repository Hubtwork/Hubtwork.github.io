---
layout: post
title: (프로그래머스 Lv1) K번째 수
subtitle: K번째 수 문제 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, sorted]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 모의고사 ( Python )
  </h2>
</center>


------

[Lv1 K번째수 Link](https://programmers.co.kr/learn/courses/30/lessons/42748)

### <span style="color:skyblue"># 문제 설명</span>

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### <span style="color:skyblue"># 제한 사항</span>

- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

### <span style="color:skyblue"># 입출력 예</span>

| array                 | commands                          | return    |
| --------------------- | --------------------------------- | --------- |
| [1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3] |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **각 command 에 맞게 array 를 자르고, 해당 인덱스의 숫자를 가져온다.**

>  입력된 commands 배열 내의 command 의 형식을 분석하자면, **[ i ( start ) , j ( end ) , k ( charAt ) ]** 으로 생각해볼 수 있다. <span style="color:skyblue">주어진 array 를 i번째부터 j번째까지 잘라 오름차순으로 정렬하고, 그 안에서 k 번째 문자를 가져오는 것이 각 커맨드의 목적</span>이다. ( <u>*주의할 것은 배열은 index 가 0 부터 시작하기 때문에 주어진 i-1 번째 요소부터 확인해야한다는 것이다.*</u> )
>
>  파싱과정은 python 의 문자열 슬라이싱과 **sorted(iterable) 함수**로 간결히 구현할 수 있다. 타겟 Iterable 을 정렬하고 별다른 객체를 반환하지 않는 Iterable.sort() 함수와 다르게,  **sorted(iterable)** 는 <span style="color:red">정렬된 이터러블을 생성하여 반환</span>한다. 
>
>  ```python
>  '''
>  	command means
>    1. parse array i-th index to j-th index
>    2. get k-th word in parsed array
>  ''' 
>  i, j, k = command
>  ar = sorted(array[i-1:j])
>  answer.append(ar[k-1])
>  ```
>  <br>
>  각 커맨드에 대해 위 과정을 시행하고 그 결과를 반환하면 된다.

<br>

### 전체 코드

```python
def solution(array, commands):
    answer = []
    # Parse array based on each command.
    for command in commands:
        '''
            command means
            1. parse array i-th index to j-th index
            2. get k-th word in parsed array
        ''' 
        i, j, k = command
        ar = sorted(array[i-1:j])
        answer.append(ar[k-1])
    return answer
```

