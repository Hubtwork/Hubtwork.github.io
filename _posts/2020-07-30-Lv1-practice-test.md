---
layout: post
title: (프로그래머스 Lv1) 모의고사
subtitle: 모의고사 문제 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, enumerate]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 모의고사 ( Python )
  </h2>
</center>

------
[Lv1 모의고사 Link](https://programmers.co.kr/learn/courses/30/lessons/42840)

### <span style="color:skyblue"># 문제 설명</span>

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### <span style="color:skyblue"># 제한 사항</span>

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

### <span style="color:skyblue"># 입출력 예</span>

| answers     | return  |
| ----------- | ------- |
| [1,2,3,4,5] | [1]     |
| [1,3,2,4,2] | [1,2,3] |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **각 수포자는 답을 찍는 방식이 정해져 있다.**

>  문제에서, 각 수포자가 문제를 찍는 방식이 정해져 있음을 알 수 있다. **1번 학생의 경우 1~5** 를 반복, **2번 학생의 경우 21,22,23,24,25**을 반복, **3번 학생의 경우 33,11,22,44,55 **를 반복 한다. 이 규칙들을 먼저 ans_sheet 로 보관한다.
>
>  ```python
>  # member count is 3.
>  score = [0 for _ in range(3)]
>  # enroll each member's answer sheet.
>  ans_sheet = []
>  ans_sheet.append([1,2,3,4,5])
>  ans_sheet.append([2,1,2,3,2,4,2,5])
>  ans_sheet.append([3,3,1,1,2,2,4,4,5,5])
>  ```
>  <br>
>  저장한 **각 수포자의 ans_sheet 를 활용해 각 수포자의 점수를 계산하는 calcScore 함수**를 만들어 점수를 계산한다. for 문 내에서 단순히 매 정답에 대해 각 ans_sheet 에 대한 계산을 해도 되지만, 가독성 높은 코드 작성을 위해 함수로 따로 분리해내어 작성하였다.  점수 계산 함수에서는  **enumerate *( iterable 에 대해 index, value 쌍을 반환 )* ** 를 활용, 각 수포자의 ans_sheet 가 반복되는 것을 쉽게 계산할 수 있도록 answer 의 idx 를 참조해 ans_sheet 를 확인할 수 있게 구현하였다.
>
>  ```python
>  # calculate score based on each member's ans_sheet 
>  def calcScore(answers, ans_sheet):
>      score = 0
>      for idx, ans in enumerate(answers):
>          if ans == ans_sheet[idx % len(ans_sheet)]:
>              score += 1
>      return score
>    
>  # calculate each members score.
>  for i in range(len(score)):
>      score[i] = calcScore(answers, ans_sheet[i])
>  ```
>  <br> 그 뒤에는 문제에 맞게 최고 점수를 구한 후 최고 점수를 가진 수포자의 index 를 반환하는 것으로 문제를 해결할 수 있다.

<br>

### 전체 코드

```python
# calculate score based on each member's ans_sheet 
def calcScore(answers, ans_sheet):
    score = 0
    for idx, ans in enumerate(answers):
        if ans == ans_sheet[idx % len(ans_sheet)]:
            score += 1
    return score
        

def solution(answers):
    answer = []
    # member count is 3.
    score = [0 for _ in range(3)]
    # enroll each member's answer sheet.
    ans_sheet = []
    ans_sheet.append([1,2,3,4,5])
    ans_sheet.append([2,1,2,3,2,4,2,5])
    ans_sheet.append([3,3,1,1,2,2,4,4,5,5])
    # calculate each members score based on answers, answer_sheet.
    for i in range(len(score)):
        score[i] = calcScore(answers, ans_sheet[i])
    # find best score of members and 
    best = max(score)
    for i in range(3):
        if score[i] == best:
            answer.append(i+1)
    return answer
```

