---
layout: post
title: Codility Python
comments: true
---

Here are my 100% solutions for Codility Lessons written in Python. Solutions are hidden (so you have few seconds to make sure that you don't want to solve task by yourself) Titles are links to description on Codility Platform. Enjoy and if you have remarks or alternative solutions - share in comments!

### 1. Iterations

### 2. Arrays

{%
    include codility.html
    url='https://codility.com/programmers/lessons/2-arrays/cyclic_rotation/'
    git='e68526c034bd1fa5371949fe9abfa61d'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/2-arrays/odd_occurrences_in_array/'
    git='1563ce7c610c9d035c749549b3edcda9'
%}

<!--
```python
def solution(A, K):
    l = len(A)
    if l == 0:
        return A
    K = K % l
    if K == 0:
        return A
    a = l
    b = K
    while b:
        a, b = b, a % b
    skip = l // a
    for j in range(0, l // skip):
        pre = A[j]
        for i in range(j, skip * K, K):
            next, A[i % l] = A[i % l], pre
            pre = next
    return A
```
-->

### 3. Time Complexity

{%
    include codility.html
    url='https://codility.com/programmers/lessons/3-time_complexity/tape_equilibrium/'
    git='e7c838862e6e09b0473ed5a105571dac'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/3-time_complexity/frog_jmp/'
    git='1d1ea33dae7d967e409e21a95bdb6dc3'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/3-time_complexity/perm_missing_elem/'
    git='6b6166d044a1a807d07f67988b0267cd'
%}

### 4. Counting Elements

{%
    include codility.html
    url='https://codility.com/programmers/lessons/4-counting_elements/perm_check/'
    git='734981f1c916a1e5263fef3a0cb3e643'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/4-counting_elements/frog_river_one/'
    git='c58ef6c61adeba70b79b76abf88bb2d5'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/4-counting_elements/missing_integer/'
    git='e939479277b82e85d29cf50ea686ef05'
%}


{%
    include codility.html
    url='https://codility.com/programmers/lessons/4-counting_elements/max_counters/'
    git='46a0a2e754d16a0f59ca0c311dcfcb16'
%}


### 5. Prefix Sums

{%
    include codility.html
    url='https://codility.com/programmers/lessons/5-prefix_sums/passing_cars/'
    git='e4e14aa909eecefcfca5df6b821e15e8'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/5-prefix_sums/count_div/'
    git='88ac7d17e3dcce00177e94c758b2a7c4'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/5-prefix_sums/min_avg_two_slice/'
    git='bd2b6dcde43b4620be670d17412b9c1e'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/5-prefix_sums/genomic_range_query/'
    git='326791cae44e77cfa093cf1ca08acfb7'
%}

### 10. Prime and composite numbers

{%
    include codility.html
    url='https://codility.com/programmers/lessons/10-prime_and_composite_numbers/peaks/'
    git='20f47851996d7fc4ad6e22ca48ef7b6b'
%}


### 11. Sieve of Eratosthenes

{%
    include codility.html
    url='https://codility.com/programmers/lessons/11-sieve_of_eratosthenes/count_semiprimes/'
    git='db218558951bc17cc079b033e5af08ac'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/11-sieve_of_eratosthenes/count_non_divisible/'
    git='841637b38f9501c9ef8fdc2d08517810'
%}

### 12. Euclidean algorithm

{%
    include codility.html
    url='https://codility.com/programmers/lessons/12-euclidean_algorithm/chocolates_by_numbers/'
    git='19f0e3f0671ee2e2070f45d874df873c'
%}

{%
    include codility.html
    url='https://codility.com/programmers/lessons/12-euclidean_algorithm/common_prime_divisors/'
    git='98bd9dc2fd459aa5dd54b829389a22c0'
%}

### 13. 

<!--

### 6. Sorting


#### 1. [MaxProductOfThree](https://codility.com/programmers/lessons/6-sorting/max_product_of_three/)
```python
def solution(A):
    A.sort()
    a = max(A[0] * A[1] * A[2], float('-inf'))
    b = max(A[0] * A[1] * A[-1], a)
    c = max(A[0] * A[-2] * A[-1], b)
    d = max(A[-3] * A[-2] * A[-1], c)
    return d    
```
#### 2. [Distinct](https://codility.com/programmers/lessons/6-sorting/distinct/)
```python
def solution(A):
    if len(A) == 0:
        return 0
    A.sort()
    result = 1
    for i in range(0, len(A)-1):
        if A[i] != A[i+1]:
            result += 1
    return result
```
#### 3. [Triangle](https://codility.com/programmers/lessons/6-sorting/triangle/)
```python
def solution(A):
    if len(A) < 3:
        return 0
    A.sort()
    for i in range(0, len(A) - 2):
        if A[i] + A[i+1] > A[i+2] and A[i] < A[i+1] + A[i+2] and A[i] + A[i+2] > A[i+2]:
            return 1
    return 0
```
#### 4. [NumberOfDiscIntersections](https://codility.com/programmers/lessons/6-sorting/number_of_disc_intersections/)
```python
def solution(A):
    if len(A) == 0:
        return 0
    l = len(A)
    B, C = [0] * l, [0] * l
    for i in range(0, l):
        left, right = i - A[i], i + A[i]
        B[left if left >= 0 else 0] += 1
        C[right if right < l else l - 1] -= 1

    acc, result = 0, 0
    for i in range(0, l):
        if result > 10000000:
            return -1
        result += B[i] * acc
        result += (B[i] * (B[i] - 1)) / 2
        acc += B[i] + C[i]
    return result

solution([1, 5, 2, 1, 4, 0])
```
### Lessons 7 - Prefix Sums

```python
def solution(S):
    if len(S) == 0:
        return 1
    A = []
    for s in S:
        num = ord(s)        
        if num == 40 or num == 91 or num == 123:
            A.append(str(unichr(num + (1 if num == 40 else 2))))
        else:
            if len(A) == 0 or A.pop() != s:
                return 0
    return 1 if len(A) == 0 else 0

solution('{[()()]}')
```
#### 2. 
```python
def solution(A, B):
    l = len(A)
    D = [] # fish swimming downstream
    alive, acctual = 0, 0
    for i in range(0, l):
        if B[i] == 1:
            D.append(A[i])
        else:
            while len(D) > 0 and D[-1] < A[i]:
                D.pop()
            alive += 1 if len(D) == 0 else 0
    return len(D) + alive

solution([4, 3, 2, 1, 5], [0, 1, 0, 0, 0])
```
#### 3. [Nesting](https://codility.com/programmers/lessons/7-stacks_and_queues/nesting/)
```python
def solution(H):
    num = 0
    A = []
    for h in H:
        if len(A) == 0 or A[-1] < h:
            A.append(h)
            num += 1
        else:
            while len(A) > 0 and A[-1] > h:
                A.pop()
            if len(A) == 0 or A[-1] < h:
                num += 1
                A.append(h)
    return num

solution([8, 8, 5, 7, 9, 8, 7, 4, 8])
```

### 8. Lesson - Leader
#### 1. [Dominator](https://codility.com/programmers/lessons/8-leader/dominator/)
```python
def solution(A):
    if len(A) == 0:
        return -1
    dom = 0
    app = 1
    for i in range(0, len(A)):
        if dom == A[i]:
            app += 1
        else:
            app -= 1
        if app == 0:
            dom = i
            app += 1
    return dom
```
#### 2. [EquiLeader](https://codility.com/programmers/lessons/8-leader/equi_leader/)
```python
def solution(A):
    dom, app = A[0], 0
    for a in A:
        app = app + (1 if dom == a else -1)
        if app == 0:
            dom = a
            app += 1
    app = 0
    for a in A:
        if a == dom:
            app += 1
    if app <= len(A) / 2:
        return 0
    else:
        num = 0
        pre = 0
        aft = app
        for i in range(0, len(A) - 1):
            if A[i] == dom:
                pre += 1
                aft -= 1
            if pre > (i + 1)/2 and aft > (len(A) - i - 1)/2:
                num += 1
        return num

solution([4, 3, 4, 4, 4, 2])
```

### 9. Lesson - ?

#### 1. 
```python
def solution(A):
    max = float('-inf')
    sum = 0
    for a in A:
        sum += a
        if sum > max:
            max = sum
        if sum < 0:
            sum = 0
    return max

solution([3, 2, -6, 4, 0])
```
#### 2. For 92%
```python
def solution(A):
    if len(A) <= 3:
        return 0

    MIN, MAX = float('-inf'), float('inf')
    suma = 0
    maks = MIN
    mini = MAX

    for i in range(1, len(A)-1):
        if A[i] < mini:
            suma += mini if mini < MAX else 0
            mini = A[i]
        else:
            suma += A[i]
        maks = max(suma, maks)
        if suma < 0:
            suma = 0
            mini = MAX
    return maks

solution([3, 2, 6, -1, 4, 5, -1, 2])
```
#### 3.
```python
def solution(A):
    mini = float('inf')
    winner = 0
    for a in A:
        winner = max(winner, a - mini)
        mini = min(mini, a)
    return winner

solution([23171, 21011, 21123, 21366, 21013, 21367])
```

### 10. Prime and composite numbers

#### 1. []()
```python
def solution(N):
    n = N ** 0.5
    result = 0
    i = 1
    while i < n:
        if N % i == 0:
            result += 2
        i += 1
    if i == n:
        result += 1
    return result

solution(24) == 8
``` python

#### 2. []()


#### 3. [Flags](https://codility.com/programmers/lessons/10-prime_and_composite_numbers/flags/)
<script src="https://gist.github.com/jonzee/29974e17ada2d07574e5c949d3353e78.js"></script>

#### 4. [Peaks](https://codility.com/programmers/lessons/10-prime_and_composite_numbers/peaks/)

### 11. Siece of Eratostenes
### 12. Euclidean algorithm
### 13. Fibonacci numbers
### 14. Binary search algorithm
### 15. Caterpillar method
### 16. Greedy algorithms
### 17. Dynamic programming
### 90. Tasks from Indeed Prime 2015 challenge
### 91. Tasks from Indeed Prime 2016 College Coders challenge
### 99. Future training


12 - 8 inch - poprzeczka 30 - 20 cm 

-->

