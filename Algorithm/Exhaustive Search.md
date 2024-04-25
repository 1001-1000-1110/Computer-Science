# Exhaustive Search

**가능한 모든 경우의 수를 탐색**해 **최적의 결과를 찾는 방법**을 의미한다. 

<img width="1250" alt="스크린샷 2024-04-25 오후 1 48 16" src="https://github.com/Heo-Jeong-Eun/TIL/assets/60500256/cab63952-06ef-4ecb-8110-baed59288fd4">

## Brute-Force

난폭한 힘, 폭력 → 무식하지만 확실한 방법을 의미한다. 

수행하는데 오랜 시간과 많은 자원을 소요하지만 이론적으로 가능한 수를 모두 검색하기에 예상한 결과를 얻을 수 있다. 

**모든 경우를 다 탐색해 결과를 얻는 알고리즘이다.** 

해당 알고리즘은 경우의 수가 작을 때 사용하는 것이 일반적이다. 

### Array Search

배열에서 특정 값을 찾는 문제에서 모든 배열을 탐색하는 방식인 Brute-Force을 사용할 수 있다.

```python
def findIndex(arr, target):
	for i in range(len(arr)):
		if arr[i] == target:
			return i
	return -1
```

### String Search

문자열 비교 문제에서 Brute-Force는 모든 문자열 쌍을 비교해 최소, 최대를 찾는 방식으로 문제를 해결한다. 

```python
def stringCompare(s1, s2):
  length_s1 = len(s1)
  length_s2 = len(s2)

  small_length = min(length_s1, length_s2)

  for i in range(small_length):
    if s1[i] != s2[i]:
      return ord(s1[i]) - ord(s2[i])

  if (length_s1 == length_s2):
    return 0
  elif length_s1 > length_s2:
    return s1[small_length]
  else:
    return s2[small_length]
```

## Bit-Mask

**이진수를 Bit 연산을 통해 경우의 수를 줄여가며 탐색하는 방식**을 의미한다. 

모든 경우의 수를 이진수로 표현, Bit-Mask를 사용하면 하나의 변수에 여러 개의 상태 정보를 저장할 수 이를 통해 복잡한 조건문을 간단하게 처리할 수 있는 장점이 있다. 

Bit 연산을 사용하기 때문에 빠른 계산이 가능해 경우의 수가 많을 때 유리하다. 

### Basic Caculation

```python
a = 10 # 1010
b = 12 # 1100

result = a & b
result = a | b
result = a ^ b # XOR 연산
result = a << 1
result = a >> 1
```

### Administering Permissions, 권한 관리

보통 권한은 4가지 이상으로 구분 되어 있는 경우가 대부분, 각 권한을 Bit로 표현해 하나의 정수 값으로 나타내면 간단하게 연산이 가능하다. 

```python
PERMISSION_READ = 0b0001 << 0; # 0001
PERMISSION_WRITE = 0b0001 << 1; # 0010
PERMISSION_DELETE = 0b0001 << 2; # 0100
PERMISSION_EXECUTE = 0b0001 << 3; # 1000

print(PERMISSION_EXECUTE)
userPermission = PERMISSION_READ | PERMISSION_WRITE
print(userPermission)
groupPermission = PERMISSION_READ | PERMISSION_EXECUTE

hasReadPermission = (userPermission & PERMISSION_READ) != 0
print(hasReadPermission)
hasDeletePermission = groupPermission & PERMISSION_DELETE != 0
print(hasDeletePermission)

#출력문
#8
#3
#True
#False
```

### Set permissions, 집합 관리

집합을 Bit로 표현해 Memory를 절약할 수 있다. 

```python
set = (1 << 3) | (1 << 5) | (1 << 7) # 0010 1010 1000
hasElement5 = (set & (1 << 5)) != 0; # True
hasElement6 = (set & (1 << 6)) != 0; # False
```

### Status Flag permissions, 상태 플래그 관리

여러 상태를 하나의 정수값으로 나타내 관리할 수 있다. 

```python
FLAG_POWER_OF_TWO = 1 << 0; # 0001
FLAG_NEGATIVE = 1 << 1; # 0010

number = 8; # 2의 거듭제곱
flags = 0;

if number & (number-1) == 0 :
    flags |= FLAG_POWER_OF_TWO

if (number < 0):
    flags |= FLAG_NEGATIVE
    print(flags)

if ((flags & FLAG_POWER_OF_TWO) != 0):
    print(number, " is power of two") # 1

if ((flags & FLAG_NEGATIVE != 0)):
    print(number, "is negaive") # 2
```

## Back-Tracking

**정답으로 가는 중 막히게 되면, 그 지점으로 다시 돌아가서 다른 경로를 탐색하는 방식**을 의미한다. 

해당 알고리즘을 사용할 떄 보통 **재귀**를 통해 구현하며, **Stack**을 이용해 구현하는 경우도 있다. 

재귀를 사용하는 경우, 구현을 위해 생성, 검사, 선택, 이동, 되돌아가기 등의 과정이 재귀적으로 수행된다. 

## Permutation Search

**순열을 이용해 모든 경우의 수를 탐색하는 방법**으로 **서로 다른 n개 중 r개를 선택해 숫자를 모든 순서대로 뽑는 것**을 말한다. 

### Permutation, 순열

```python
[1,2]
[1,3]
[2,1]
[2,3]
[3.1]
```

### Swap Array Permutation

![img](https://github.com/Heo-Jeong-Eun/TIL/assets/60500256/a51ac629-d7b5-45d4-9432-4f78430ca004)

Swap Array 

**배열에서 두 요소의 위치를 바꿔가며 순열을 생성하는 방법**이다. 

배열의 index 0부터 순서대로 선택하면 다음 index와 위치를 바꾸고 마지막 index까지 반복한다. 

쉽게 구현이 가능하지만 큰 Dataset의 경우 **비효율적인 방법**이다. 

```python
class Permutation():
  # permute : 순열의 로직을 수행합니다.
  def permute(self, arr, k):
    for i in range(k, len(arr)):
      self.swap(arr, i, k)
      self.permute(arr, k+1)
      self.swap(arr, k, i)

    if (k == len(arr)-1):
      print(arr)

  # swap : 배열의 요소 값을 Swap 합니다.
  def swap(self, arr, i, j):
    """

    :param arr: 배열
    :param i: 현재 인덱스
    :param j: 바꿀 인덱스
    :return:
    """
    tmp = arr[i]
    arr[i] = arr[j]
    arr[j] = tmp

def main():
  arr = [1, 2, 3, 4]
  p = Permutation()

  p.permute(arr, 0)

if __name__ == '__main__':
  main()
```

1. main에서 permute method에서 parameter로 배열과 0개를 선택
2. permute는 재귀적으로 호출하며 swap method를 이용해 배열의 원소를 순서대로 바꾸면서 모든 순열을 생성한다. 
3. 이때, k는 순열을 생성할 위치를 의미한다. 만약 k가 arr의 길이와 같아지면 모든 원소에 대한 순열이 생성되는 것을 의미하므로 순열을 출력한다. 

**즉, 순열에서 특정 값을 고정시키고 이후 값들을 swap하면서 순열을 생성한다.** 

### Visited Array Permutation

배열에서 현재 index 값을 선택한 후 해당 index를 visited라는 배열에 표시한다. 

이후 다음 index로 넘어가기 전 visited 배열에 표시되지 않은 가장 작은 index를 선택한다. 

위 과정을 마지막 index까지 반복한다. 

이 방법은 swap보다 효율적이다. 

![img](https://github.com/Heo-Jeong-Eun/TIL/assets/60500256/ab9240bd-1fb2-4798-86fa-bbb659ec30c6)

**하나의 Loop 안에서 해당 index가 visited이면 다음 최소 index로 넘어간다.** 

## Recursive Function

**함수 내부에서 자기 자신을 호출하는 함수**를 의미한다. 함수가 자신을 반복적으로 호출하며 원하는 결과를 도출할 수 있다. 

## DFS, BFS

DFS, BFS는 **비선형 구조에서 주로 사용**되고, 선형 구조에서는 큰 의미를 갖지 않는다. 

### DFS

**Root Node에서 시작, 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법**을 의미한다. 

**Stack, Recursive**를 이용해 구현할 수 있다. 

### BFS

**Root Node에서 시작해 인접한 Node를 먼저 탐색하는 방법**을 의미한다. 

**Queue**를 이용해 구현이 가능하다. 

|  | DFS | BFS |
| :---: | :---: | :---: |
| Data Structure | Stack | Queue |
| Search Way | Depth First | Width First |
| Shortest Path Search | X | O |
| Recursive Implementation Possible | O | X |
| Repeatable Sentence Implementable | X | O |
| Memory Usage | Few | Lot |