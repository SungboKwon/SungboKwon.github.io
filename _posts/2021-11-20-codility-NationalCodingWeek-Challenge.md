---
layout: post
title: Codility National Coding Week Challenge
subtitle: Problem Solving Log
categories: coding-challenge
tags: [challenge, codility]
---

You can find 'Task Description' in [Codility Challenge](https://app.codility.com/programmers/challenges/national_coding_week_2021/).

I worked for ended challenge just for fun, and got 100% score. And sharing my solution.

## Main Concept
쉽게 String의 character를 변환하기 위해 char array에 input을 저장합니다.

'abb' -> 'baa'의 변환을 하는 문제입니다.
b = 1, a = 0이라고 생각하면 011 -> 100으로 바꾸는, 즉 1을 더하는 변환입니다.
따라서 뒤에서 앞으로 변환을 진행하면 O(N)의 복잡도로 문제를 해결할 수 있습니다.

단, "abbbbbb"와 같은 문자열이 나타난다면 앞에서 뒤로 변환을 수행할 필요가 있습니다.
"abbbbbb" -> "baabbbb" -> "babaabb" -> "bababaa"

iteration을 뒤에서 앞으로 반복하며 'abb'패턴을 탐색합니다.
'abb'패턴을 찾으면 이를 'baa'로 바꾼 후 해당 지점부터 이어지는 'abb'가 더이상 없을 때 까지만 앞에서 뒤로 탐색을 수행합니다.

## Computational Complexity (Big-O)
**O(N)** for worst/general/best cases.

<- 방향 iteration 속에 -> 방향 iteration이 존재하기 때문에
$O(N^2)$
의 복잡도를 갖는다고 착각할 수 있습니다.
하지만 ->방향 iteration은 반복되는 'b'문자에 대해서만 수행하고, 반복되는 'b'문자에 대해 한 번의 iteration을 수행하면 해당 반복이 사라져 재 탐색을 하지 않아도 됩니다. 따라서 <-방향 iteration이 N, ->방향 iteration이 worst case N으로 N + N의 복잡도를 갖게 되고, 결국 worst case에도 O(N)이 됩니다.
