---
layout: post
title: Codility Python
---

Algorythms from codility lessons writed in Python.

{% gist 5555251 %}

### Lesson 1
```python
def solution(A):

```


### Lesson 2 - Arrays

#### 1. OddOccurrencesInArray

<script src="https://gist.github.com/jonzee/1563ce7c610c9d035c749549b3edcda9.js"></script>

#### 2. CyclicRotation

{% gist 1563ce7c610c9d035c749549b3edcda9 %}

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
```python
def reverse(A, i, j):
    while i < j:
        A[i], A[j], i, j = A[j], A[i], i+1, j-1
        
def solution(A, K):
    l = len(A)
    K = K % l
    if l == 0 || K == 0:
        return A

    reverse(A, 0, l - K - 1)
    reverse(A, l - K, l - 1)
    reverse(A, 0, l - 1)

```
### Lesson 3 - Time Complexity

#### 1. [TapeEquilibrium](https://codility.com/programmers/lessons/3-time_complexity/tape_equilibrium/)

```python
def solution(A):
    B = list(A)
    l = len(A)
    for i in range(1, l):
        A[i] += A[i-1]
        B[l-i-1] += B[l-i]
    m = 100000000
    for i in range(0, l - 1):
        m = min(m, abs(A[i] - B[i+1]))
    return m
```

#### 2. [FrogJmp](https://codility.com/programmers/lessons/3-time_complexity/frog_jmp/)
```python
def solution(X, Y, D):
    if (Y - X) % D != 0:
        return 1 + ((Y - X)) // D
    else:
        return ((Y - X)) // D
```

#### 3. [PermMissingElem](https://codility.com/programmers/lessons/3-time_complexity/perm_missing_elem/)
```python
def solution(A):
    tmp = 0
    l = len(A)
    for i in range(0, l):
        tmp = tmp ^ A[i] ^ (i+1)
    return tmp ^ l+1
```


### Lessons 4 - Counting Elements

#### 1. [PermCheck](https://codility.com/programmers/lessons/4-counting_elements/perm_check/)
```python
def solution(A):
    l = len(A)
    B = [0] * l
    for a in A:
        if a <= l:
            B[a-1] += 1
    for b in B:
        if b != 1:
            return 0
    return 1
```

#### 2. [FrogRiverOne](https://codility.com/programmers/lessons/4-counting_elements/frog_river_one/)
```python
def solution(X, A):
    l = len(A)
    if X > l:
        return -1
    B = [0] * (X+1)
    all = 0
    for i in range(0, l):
        if B[A[i]] == 0:
            B[A[i]] += 1
            all += 1
        if all == X:
            return i
    return -1
```

#### 3. [MissingInteger](https://codility.com/programmers/lessons/4-counting_elements/missing_integer/)
```python
def solution(A):
    l = len(A)
    B = [0] * (l + 1)
    for a in A:
        if a > 0 and a < l+1:
            B[a-1] += 1
    for i in range(0, l+1):
        if B[i] == 0:
            return i
```
#### 4. [MaxCounters](https://codility.com/programmers/lessons/4-counting_elements/max_counters/)
```python
def solution(N, A):
    C = [0] * N
    pre_max = 0
    acc_max = 0
    for a in A:
        if a == N+1:
            acc_max = pre_max
        else:
            if C[a-1] < acc_max:
                C[a-1] = acc_max + 1
            else:
                C[a-1] += 1
            pre_max = max(pre_max, C[a-1])
    for i in range(0, len(C)):
        C[i] = max(acc_max, C[i])
    return C
```
### Lessons 5 - Prefix Sums

#### 1. [PassingCars](https://codility.com/programmers/lessons/5-prefix_sums/passing_cars/)
```python
def solution(A):
    est = 0
    res = 0
    for a in A:
        if a == 0:
            est += 1
        else:
            res += est
        if res > 1000000000:
            return -1
    return res


```
#### 2. [CountDiv](https://codility.com/programmers/lessons/5-prefix_sums/count_div/)
```python
def solution(A, B, K):
    return (B - A + 1) // K
```

#### 3. [MinAvgTwoSlice](https://codility.com/programmers/lessons/5-prefix_sums/min_avg_two_slice/)
```python
def solution(A):
    l = len(A)
    minimum = 100000
    result = 0
    for i in range(0, l):
        if i + 1 < l:
            tmp = (A[i] + A[i+1]) / 2.
            if tmp < minimum:
                minimum, result = tmp, i 
        if i + 2 < l:
            tmp = (A[i] + A[i+1] + A[i+2]) / 3.
            if tmp < minimum:
                minimum, result = tmp, i 
    return result
```
### 4. [GenomicRangeQuery](https://codility.com/programmers/lessons/5-prefix_sums/genomic_range_query/)
```python
def solution(S, P, Q):
    l = len(S)
    D = [[0 for x in range(l)] for y in range(4)]
    A = 100001
    C = 100001
    G = 100001
    T = 100001
    for i in range(l-1, -1, -1):
        if S[i] == 'A':
            A = i
        if S[i] == 'C':
            C = i
        if S[i] == 'G':
            G = i
        if S[i] == 'T':
            T = i
        D[0][i] = A
        D[1][i] = C
        D[2][i] = G
        D[3][i] = T
    r = len(P)
    W = [0] * r
    for i in range(0, r):
        if D[0][P[i]] <= Q[i]:
            W[i] = 1
            continue
        if D[1][P[i]] <= Q[i]:
            W[i] = 2
            continue
        if D[2][P[i]] <= Q[i]:
            W[i] = 3
            continue
        if D[3][P[i]] <= Q[i]:
            W[i] = 4
    return W

solution('CAGCCTA', [2, 5, 0], [4, 5, 6])
```
### Lessons 6 - Sorting
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

### 10. Lesson - 

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