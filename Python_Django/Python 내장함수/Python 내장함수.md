# Python 내장함수

---

- 내장함수 리스트 바로가기

---

### abs

abs(x)는 어떤 숫자를 입력받았을 때, 그 숫자의 절댓값을 돌려주는 함수이다.

```python
>>> abs(3)
3
>>> abs(-3)
3
>>> abs(-1.2)
1.2
```

### all

all(x)는 반복 가능한(iterable) 자료형 x를 입력 인수로 받으며 이 x가 모두 참이면 True, 거짓이 하나라도 있으면 False를 돌려준다.

```python
>>> all([1, 2, 3])
True
# 리스트 자료형 [1, 2, 3]은 모든 요소가 참이므로 True를 돌려준다.

>>> all([1, 2, 3, 0])
False
# 리스트 자료형 [1, 2, 3, 0] 중에서 요소 0은 거짓이므로 False를 돌려준다.
```

### any

any(x)는 x 중 하나라도 참이 있으면 True를 돌려주고, x가 모두 거짓일 때에만 False를 돌려준다. all(x)의 반대이다.

```python
>>> any([1, 2, 3, 0])
True
# 리스트 자료형 [1, 2, 3, 0] 중에서 1, 2, 3이 참이므로 True를 돌려준다.

>>> any([0, ""])
False
# 리스트 자료형 [0, ""]의 요소 0과 ""은 모두 거짓이므로 False를 돌려준다.
```

### chr

chr(i)는 아스키(ASCII) 코드 값을 입력받아 그 코드에 해당하는 문자를 출력하는 함수이다.

※ 아스키 코드란 0에서 127 사이의 숫자를 각각 하나의 문자 또는 기호에 대응시켜 놓은 것이다.

```python
>>> chr(97)
'a'
>>> chr(48)
'0'
```

### dir

dir은 객체가 자체적으로 가지고 있는 변수나 함수를 보여 준다. 다음 예는 리스트와 딕셔너리 객체 관련 함수(메서드)를 보여 주는 예이다.

```python
>>> dir([1, 2, 3])
['append', 'count', 'extend', 'index', 'insert', 'pop',...]
>>> dir({'1':'a'})
['clear', 'copy', 'get', 'has_key', 'items', 'keys',...]
```

### divmod

divmod(a, b)는 2개의 숫자를 입력으로 받는다. 그리고 a를 b로 나눈 몫과 나머지를 튜플 형태로 돌려주는 함수이다.

```python
>>> divmod(7, 3)
(2, 1)
# 몫을 구하는 연산자 //와 나머지를 구하는 연산자 %를 각각 사용한 결과와 비교해 보자.

>>> 7 // 3
2
>>> 7 % 3
1
```

### enumerate

enumerate는 "열거하다"라는 뜻이다. 이 함수는 순서가 있는 자료형(리스트, 튜플, 문자열)을 입력으로 받아 인덱스 값을 포함하는 enumerate 객체를 돌려준다.

```python
>>> for i, name in enumerate(['body', 'foo', 'bar']):
...     print(i, name)
...
0 body
1 foo
2 bar
```

### eval

eval(expression)은 실행 가능한 문자열(1+2, 'hi' + 'a' 같은 것)을 입력으로 받아 문자열을 실행한 결괏값을 돌려주는 함수이다.

```python
>>> eval('1+2')
3
>>> eval("'hi' + 'a'")
'hia'
>>> eval('divmod(4, 3)')
(1, 1)
```

보통 eval은 입력받은 문자열로 파이썬 함수나 클래스를 동적으로 실행하고 싶을 때 사용한다.

### filter

filter 함수는 첫 번째 인수로 함수 이름을, 두 번째 인수로 그 함수에 차례로 들어갈 반복 가능한 자료형을 받는다. 그리고 두 번째 인수인 반복 가능한 자료형 요소가 첫 번째 인수인 함수에 입력되었을 때 반환 값이 참인 것만 묶어서(걸러 내서) 돌려준다.

```python
def positive(x):
    return x > 0

print(list(filter(positive, [1, -3, 2, 0, -5, 6])))
# 결과값: [1, 2, 6]

>>> list(filter(lambda x: x > 0, [1, -3, 2, 0, -5, 6]))
[1, 2, 6]
```

### hex

hex(x)는 정수 값을 입력받아 16진수(hexadecimal)로 변환하여 돌려주는 함수이다.

```python
>>> hex(234)
'0xea'
>>> hex(3)
'0x3'
```

### id

id(object)는 객체를 입력받아 객체의 고유 주소 값(레퍼런스)을 돌려주는 함수이다.

```python
>>> a = 3
>>> id(3)
135072304
>>> id(a)
135072304
>>> b = a
>>> id(b)
135072304
>>> id(4)
135072292
```

위 예의 3, a, b는 고유 주소 값이 모두 135072304이다. 즉 3, a, b가 모두 같은 객체를 가리키고 있다.
만약 id(4)라고 입력하면 4는 3, a, b와 다른 객체이므로 당연히 다른 고유 주소 값이 출력된다.

### input

input(\[prompt\])은 사용자 입력을 받는 함수이다. 매개변수로 문자열을 주면 다음 세 번째 예에서 볼 수 있듯이 그 문자열은 프롬프트가 된다.

```python
>>> a = input()
hi
>>> a
'hi'
>>> b = input("Enter: ")
Enter: hi

>>> b
'hi'
```

### int

int(x)는 문자열 형태의 숫자나 소수점이 있는 숫자 등을 정수 형태로 돌려주는 함수로, 정수를 입력으로 받으면 그대로 돌려준다.

```python
>>> int('3')
3
>>> int(3.4)
3
# int(x, radix)는 radix 진수로 표현된 문자열 x를 10진수로 변환하여 돌려준다.

# 2진수로 표현된 11의 10진수 값은 다음과 같이 구한다.

>>> int('11', 2)
3
# 16진수로 표현된 1A의 10진수 값은 다음과 같이 구한다.

>>> int('1A', 16)
26
```

### isinstance

isinstance(object, class)는 첫 번째 인수로 인스턴스, 두 번째 인수로 클래스 이름을 받는다. 입력으로 받은 인스턴스가 그 클래스의 인스턴스인지를 판단하여 참이면 True, 거짓이면 False를 돌려준다.

```python
>>> class Person: pass
...
>>> a = Person()
>>> isinstance(a, Person)
True
# 위 예는 a가 Person 클래스가 만든 인스턴스임을 확인시켜 준다.

>>> b = 3
>>> isinstance(b, Person)
False
# b는 Person 클래스가 만든 인스턴스가 아니므로 False를 돌려준다.
```

### len

len(s)은 입력값 s의 길이(요소의 전체 개수)를 돌려주는 함수이다.

```python
>>> len("python")
6
>>> len([1,2,3])
3
>>> len((1, 'a'))
2
```

### list

list(s)는 반복 가능한 자료형 s를 입력받아 리스트로 만들어 돌려주는 함수이다.

```python
>>> list("python")
['p', 'y', 't', 'h', 'o', 'n']
>>> list((1,2,3))
[1, 2, 3]
# list 함수에 리스트를 입력으로 주면 똑같은 리스트를 복사하여 돌려준다.

>>> a = [1, 2, 3]
>>> b = list(a)
>>> b
[1, 2, 3]
```

### map

map(f, iterable)은 함수(f)와 반복 가능한(iterable) 자료형을 입력으로 받는다. map은 입력받은 자료형의 각 요소를 함수 f가 수행한 결과를 묶어서 돌려주는 함수이다.

```python
>>> def two_times(x): 
...     return x*2
...
>>> list(map(two_times, [1, 2, 3, 4]))
[2, 4, 6, 8]

>>> list(map(lambda a: a*2, [1, 2, 3, 4]))
[2, 4, 6, 8]
```

- max
max(iterable)는 인수로 반복 가능한 자료형을 입력받아 그 최댓값을 돌려주는 함수이다.

```python
>>> max([1, 2, 3])
3
>>> max("python")
'y'
```

### min

min(iterable)은 max 함수와 반대로, 인수로 반복 가능한 자료형을 입력받아 그 최솟값을 돌려주는 함수이다.

```python
>>> min([1, 2, 3])
1
>>> min("python")
'h'
```

### oct

oct(x)는 정수 형태의 숫자를 8진수 문자열로 바꾸어 돌려주는 함수이다.

```python
>>> oct(34)
'0o42'
>>> oct(12345)
'0o30071'
```

### open

open(filename, [mode])은 "파일 이름"과 "읽기 방법"을 입력받아 파일 객체를 돌려주는 함수이다. 읽기 방법(mode)을 생략하면 기본값인 읽기 전용 모드(r)로 파일 객체를 만들어 돌려준다.

[open의 mode 옵션](Python%20dad8992eb22547dfa5b5d91f614cd364/open%20mode%207d171953a79240868d96f5cdba5b4336.csv)

```python
# 바이너리 읽기 모드
>>> f = open("binary_file", "rb")
>>> fread = open("read_mode.txt", 'r')
```

### ord

ord(c)는 문자의 아스키 코드 값을 돌려주는 함수이다.

※ ord 함수는 chr 함수와 반대이다.

```python
>>> ord('a')
97
>>> ord('0')
48
```

### pow

pow(x, y)는 x의 y 제곱한 결괏값을 돌려주는 함수이다.

```python
>>> pow(2, 4)
16
>>> pow(3, 3)
27
```

### range

range(\[start,\] stop \[,step\] )는 for문과 함께 자주 사용하는 함수이다. 이 함수는 입력받은 숫자에 해당하는 범위 값을 반복 가능한 객체로 만들어 돌려준다.

시작 숫자를 지정해 주지 않으면 range 함수는 0부터 시작한다.

```python
>>> list(range(5))
[0, 1, 2, 3, 4]

>>> list(range(5, 10))
[5, 6, 7, 8, 9]

>>> list(range(1, 10, 2))
[1, 3, 5, 7, 9]
>>> list(range(0, -10, -1))
[0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
```

### round

round(number\[n, digits\]) 함수는 숫자를 입력받아 반올림해 주는 함수이다.

```python
>>> round(4.6)
5
>>> round(4.2)
4
# 다음과 같이 실수 5.678을 소수점 2자리까지만 반올림하여 표시할 수 있다.

>>> round(5.678, 2)
5.68
# round 함수의 두 번째 매개변수는 반올림하여 표시하고 싶은 소수점의 자릿수(ndigits)이다.
```

- sorted
sorted(iterable) 함수는 입력값을 정렬한 후 그 결과를 리스트로 돌려주는 함수이다.

```python
>>> sorted([3, 1, 2])
[1, 2, 3]
>>> sorted(['a', 'c', 'b'])
['a', 'b', 'c']
>>> sorted("zero")
['e', 'o', 'r', 'z']
>>> sorted((3, 2, 1))
[1, 2, 3]
```

### str

str(object)은 문자열 형태로 객체를 변환하여 돌려주는 함수이다.

```python
>>> str(3)
'3'
>>> str('hi')
'hi'
>>> str('hi'.upper())
'HI'
```

### sum

sum(iterable) 은 입력받은 리스트나 튜플의 모든 요소의 합을 돌려주는 함수이다.

```python
>>> sum([1,2,3])
6
>>> sum((4,5,6))
15
```

### tuple

tuple(iterable)은 반복 가능한 자료형을 입력받아 튜플 형태로 바꾸어 돌려주는 함수이다. 만약 튜플이 입력으로 들어오면 그대로 돌려준다.

```python
>>> tuple("abc")
('a', 'b', 'c')
>>> tuple([1, 2, 3])
(1, 2, 3)
>>> tuple((1, 2, 3))
(1, 2, 3)
```

### type

type(object)은 입력값의 자료형이 무엇인지 알려 주는 함수이다.

```python
>>> type("abc")
<class 'str'>
>>> type([ ])
<class 'list'>
>>> type(open("test", 'w'))
<class '_io.TextIOWrapper'>
```

### zip

zip(\*iterable)은 동일한 개수로 이루어진 자료형을 묶어 주는 역할을 하는 함수이다.
만약 두 자료형의 개수가 동일하지 않으면, 짧은 자료형의 개수만큼 묶는다.

```python
>>> list(zip([1, 2, 3], [4, 5, 6]))
[(1, 4), (2, 5), (3, 6)]
>>> list(zip([1, 2, 3], [4, 5, 6], [7, 8, 9]))
[(1, 4, 7), (2, 5, 8), (3, 6, 9)]
>>> list(zip("abc", "def"))
[('a', 'd'), ('b', 'e'), ('c', 'f')]
```

> 출처: '점프 투 파이썬 - 내장함수' [[https://wikidocs.net/32](https://wikidocs.net/32)]