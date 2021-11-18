---
layout: post
title: Codility Spooktober Challenge
subtitle: Gold Award Log
categories: Coding Challenge
tags: [challenge][codility][gold award]
---

[Award Link](https://app.codility.com/cert/view/certVQ26T5-7ERYKYPG57AZP87U/)

You can find 'Task Description' in [Codility Challenge](https://app.codility.com/programmers/challenges/spooktober_2021/) or in 'Review detailed assessment' of [Award Link](https://app.codility.com/cert/view/certVQ26T5-7ERYKYPG57AZP87U/).

## Main Concept
각 stack의 coin은 한 step 좌우로 이동할 때 마다 절반으로 감소합니다.
| 2nd step | 1st step | start | 1st step | 2nd step |
| 1 <- | 2 <- | 5 | -> 2 | -> 1 |

stack 별로 coin의 이동을 구하여 stack 별로 합산합니다.
| stack | 1st stack | 2nd stack | 3nd stack | 4th stack | 5th stack |
| original | 1 | 2 | 0 | 4 | 2 |
| 1st stack | 1 | -> 0 | -> 0 | -> 0 | -> 0 |
| 2nd stack | 1 <- | 2 | -> 1 | -> 0 | -> 0 |
| 3rd stack | 0 <- | 0 <- | 0 | -> 0 | -> 0 |
| 4th stack | 0 <- | 1 <- | 2 <- | 4 | -> 2 |
| 5th stack | 0 <- | 0 <- | 0 <- | 1 <- | 2 |
| total | 2 | 3 | 3 | 5 | 4 |

위 합산 중 최대값을 가진 stack의 coin 수가 해답이 됩니다.

## Computational Complexity (Big-O)
**O(N)** for worst/general/best cases.
