---
layout: post
title: (프로그래머스 Lv1) 완주하지 못한 선수
subtitle: 완주하지 못한 선수 문제 풀이
cover-img: /assets/img/path.jpg
tags: [프로그래머스, Lv1, python, zip]
category: 프로그래머스
---

<center>
  <h2>
    Lv1. 완주하지 못한 선수 ( Python )
  </h2>
</center>

------
[Lv1 완주하지 못한 선수 link](https://programmers.co.kr/learn/courses/30/lessons/42576) 
<br>
### <span style="color:skyblue"># 문제 설명</span>

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다. 마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### <span style="color:skyblue"># 제한 사항</span>

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

### <span style="color:skyblue"># 입출력 예</span>

| participant                             | completion                       | return |
| --------------------------------------- | -------------------------------- | ------ |
| [leo, kiki, eden]                       | [eden, kiki]                     | leo    |
| [marina, josipa, nikola, vinko, filipa] | [josipa, filipa, marina, nikola] | vinko  |
| [mislav, stanko, mislav, ana]           | [stanko, ana, mislav]            | mislav |

<br>

 **본 문제에서 신경써야 할 것은 다음과 같다.**

- **완주하지 못한 선수는 어떤 경우에서든 한 명*( 참가자 : n , 완주자 : n-1 )***

>  마라톤 경주는 n 명의 참가자와 n-1 명의 완주자로 구성되며, 동명이인이 있을 수 있다.  즉, <span style="color:red">완주자 명단은 참가자 명단에서 완주하지 못한 사람 1명만을 제외한 목록</span> 이다. 이에 착안해 아래와 같이 두 목록을 오름차순으로 ***sort()*** 한다. sort 후에 한개씩 비교를 해 나가는데, 만일 **참가자가 마라톤을 완주했다면 같은 인덱스의 완주자 목록에도 있을 것** 이다. 반대로 **완주하지 못 했다면 두 목록의 해당 인덱스의 이름은 다를 것** 이다. 
>
> ~~~python
> '''
> after Sort, arrays will be like...
> participant : A, B, B, C, D, E
> completion : A, B, B, D, E
> 
> In 4th index, participant is C . so if C completed marathon, completion must be C.
> but completion is D, so it means C can't complete marathon.
> '''
> participant.sort()
> completion.sort()
> ~~~
>
> <br>즉, 두 목록의 이름이 달라지는 인덱스를 찾은 후 해당 인덱스의 참가자를 반환하면 된다. 서로 다른 두 배열의 인덱스를 확인하기 위해 내장함수 **zip(*iterables)** 를 활용하였다. zip 함수는 서로 다른 배열의 같은 인덱스 요소끼리 튜플로 만들고 이를 리스트로  반환해준다. 주의해야할 점은 <u>인자 중 가장 짧은 이터러블의 길이만큼만 튜플 생성 과정이 진행</u> 된다. 이를 이용해 **소팅된 튜플 중, 정답을 리턴하지 못했다면 참가자 목록의 마지막 참가자가 완주하지 못 했다는 것이므로 이를 반환**한다.
>
> ```python
> # check all zipped tuple either same or not.
> for p, c in zip(participant, completion):
>   	# if member of tuple is not same, it's answer.
>     if p != c:
>         return p
> # if result is last one, upper proccess can't find. 
> return participant[-1]
> ```
>
> 

<br>

### 전체 코드

```python
def solution(participant, completion):
  '''
after Sort, arrays will be like...
participant : A, B, B, C, D, E
completion : A, B, B, D, E

In 4th index, participant is C . so if C completed marathon, completion must be C.
but completion is D, so it means C can't complete marathon.
'''
    participant.sort()
    completion.sort()
    # check all zipped tuple either same or not.
		for p, c in zip(participant, completion):
  	# if member of tuple is not same, it's answer.
    		if p != c:
        		return p
		# if result is last one, upper proccess can't find. 
		return participant[-1]
```

