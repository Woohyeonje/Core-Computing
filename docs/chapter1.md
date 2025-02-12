#1 기본자료형과 입출력

## 1.1 기본자료형, 연산자, 변수


### 1.1.1 기본자료형

| 자료형        | 예제                     |
| ---------- | ---------------------- |
| 정수(int)    | `a = 10`               |
| 실수(float)  | `b = 3.14`             |
| 문자열(str)   | `c = "Hello"`          |
| 불리언(bool)  | `d = True`             |
| 리스트(list)  | `e = [1, 2, 3]`        |
| 튜플(tuple)  | `f = (1, 2, 3)`        |
| 딕셔너리(dict) | `g = {"key": "value"}` |
| 집합(set)    | `h = {1, 2, 3}`        |

실습 1: 기본자료형을 확인해 보자.

  ```python
  # 기본자료형 확인
  x = 10
  print(type(x))
  y = 3.14
  print(type(y))
  z = "Python"
  print(type(z))
  ```
* 실수형(float) 데이터의 특징
  - 파이썬의 실수형(float)은 소수점을 포함하는 숫자를 나타낸다.
  - 실수형은 부동소수점 방식으로 저장되므로, 정밀도 문제로 인해 연산 시 오차가 발생할 수 있다.

  * **부동소수점 방식과 정밀도 문제**

    * 부동소수점 표현 방식
      - 파이썬의 `float` 타입은 IEEE 754 표준의 64비트 부동소수점 형식을 따른다.
      - 64비트 중 1비트는 부호(sign), 11비트는 지수(exponent), 52비트는 가수(mantissa)로 구성된다.
      <그림 추가>

    * 정밀도 문제의 원인
      - 대부분의 십진수 실수는 이진수로 정확하게 표현되지 않는다.
      - 예를 들어, `0.1`은 이진수로 변환하면 무한소수(`0.00011001100110011...`)가 되어 정확히 저장되지 않는다.
      - 이로 인해 연산 시 작은 오차가 발생할 수 있다.

    * 실제 발생하는 오류 예제

      ```python
      x = 0.1 + 0.2
      print(x)  # 0.30000000000000004
      print(x == 0.3)  # False
      ```

    * 오차 해결 방법
      - `decimal` 모듈을 사용하여 정밀도를 높일 수 있다.
      - `fractions` 모듈을 사용하여 정확한 분수 연산을 수행할 수도 있다.
      - 부동소수점 연산 비교 시 **엡실론(epsilon) 판단법**을 활용할 수 있다.
        - 부동소수점 연산의 오차를 고려하여 두 실수가 충분히 가까운지를 판단할 때, 절대 오차를 이용하는 방법이다.   

     
  ```python
  # decimal 모듈 활용
  from decimal import Decimal
  x = Decimal("0.1") + Decimal("0.2")
  print(x)  # 0.3


  # fractions 모듈 활용
  from fractions import Fraction

  x = Fraction(1, 10) + Fraction(2, 10)
  print(x)  # 3/10

  # 엡실론(Epsilon) 판단법을 활용한 비교
  import math

  def is_close(a, b, epsilon=1e-9):
      return math.fabs(a - b) < epsilon

  x = 0.1 + 0.2
  y = 0.3

  print(is_close(x, y))  # True

  # `math.isclose()`를 활용
  x = 0.1 + 0.2
  y = 0.3
  print(math.isclose(x, y, rel_tol=1e-9))  # True
  ```



* 문자열

문자열은 작은따옴표(`'`)나 큰따옴표(`"`)로 둘러싸서 나타낸다.

```python
text1 = '안녕하세요'  # 작은따옴표 사용
text2 = "반갑습니다"  # 큰따옴표 사용
```

  * 여러 줄 문자열   
  파이썬에서는 삼중 따옴표(`'''` 또는 `"""`)를 사용하여 여러 줄에 걸쳐 문자열을 만들 수 있다. 이 방법은 긴 텍스트나 주석을 작성할 때 유용하다.

  ```python
  text = '''안녕하세요.
  반갑습니다.'''
  ```

  * 문자열 인덱싱   
  파이썬의 문자열은 **시퀀스 데이터**이기 때문에, 각 문자는 **인덱스 번호**로 접근할 수 있다. 인덱스 번호는 0부터 시작하며, 뒤에서부터 접근하려면 음수 인덱스를 사용할 수 있다.

  ```python
  text = "Python"
  print(text[0])  # 'P' (첫 번째 문자)
  print(text[-1]) # 'n' (마지막 문자)
  ```

  * 문자열 슬라이싱  
  슬라이싱을 사용하면 문자열의 일부분을 잘라낼 수 있다.   
  `[start:end]` 형식으로 지정하며, `start`는 시작 인덱스, `end`는 종료 인덱스를 의미합니다. `start`는 포함되지만, `end`는 포함되지 않는다.

  ```python
  print(text[0:3])  # 'Pyt' (0부터 3 미만까지)
  print(text[:3])   # 'Pyt' (처음부터 3 미만까지)
  print(text[3:])   # 'hon' (3부터 끝까지)
  ```

  슬라이싱에서 `start`, `end`, `step`을 모두 지정할 수도 있다.

  ```python
  print(text[::2])  # 'Ph' (두 칸씩 건너뛰어)
  ```

  * 문자열 연결
  두 개 이상의 문자열을 연결할 때는 `+` 연산자를 사용할 수 있다. 이 연산자를 이용하여 문자열을 합칠 수 있다.

  ```python
  greeting = "Hello"
  name = "World"
  print(greeting + " " + name)  # "Hello World"
  ```

  * 문자열 반복   
  문자열에 `*` 연산자를 사용하면 문자열을 반복할 수 있다. 이를 통해 특정 문자열을 여러 번 출력하거나 반복되는 텍스트를 만들 수 있다.

  ```python
  print("Hello! " * 3)  # "Hello! Hello! Hello!"
  ```
  * 문자열 메소드   

    * 문자열 길이   
    `len()` 함수는 문자열의 **길이**, 즉 문자열에 포함된 문자 수를 반환한다.

      ```python
      text = "Python"
      print(len(text))  # 6
      ```

    * 대소문자 변경   
      - `lower()`는 문자열을 모두 소문자로 변환한다.
      - `upper()`는 문자열을 모두 대문자로 변환한다.

      ```python
      print(text.lower())  # "python"
      print(text.upper())  # "PYTHON"
      ```
    * 공백 제거   
    문자열의 앞뒤에 불필요한 공백이 있을 수 있다. `strip()` 메소드를 사용하면 문자열의 앞뒤 공백을 제거할 수 있다.

      ```python
      text = "  Hello World  "
      print(text.strip())  # "Hello World"
      ```
    * 특정 문자 찾기   
    `find()` 메소드는 문자열 내에서 특정 문자가 처음 등장하는 **인덱스**를 반환한다. 만약 해당 문자가 없으면 `-1`을 반환

      ```python
      text = "Python"
      print(text.find('t'))  # 2 (문자 't'가 2번 인덱스에 있음)
      ```

* 포매팅

  * `f-string`을 이용한 문자열 포매팅   
  `f-string`은 파이썬 3.6 이상에서 사용 가능한 문자열 포매팅 방법이다. 문자열 안에 `{}` 중괄호를 사용하여 변수나 표현식을 삽입할 수 있다.

    ```python
    name = "Alice"
    age = 25
    print(f"이름: {name}, 나이: {age}")  # 이름: Alice, 나이: 25
    ```
  * `format()` 메소드 사용   
  `f-string`이 도입되기 전에 많이 사용되던 방법은 `format()` 메소드를 이용한 문자열 포매팅이다. 중괄호 `{}`에 변수를 삽입하고, `format()` 함수로 값을 전달한다.

    ```python
    print("이름: {}, 나이: {}".format(name, age))  # 이름: Alice, 나이: 25
    ```

---

### 6. 문자열 함수 예제(수정)

#### 6.1 문제 1: 문자열에서 첫 번째 공백 위치 찾기
`find()` 메소드를 사용하여 문자열에서 첫 번째 공백의 위치를 찾을 수 있습니다.

```python
sentence = "Hello World"
first_space = sentence.find(' ')  # 공백의 위치를 찾기
print(first_space)  # 5
```

#### 6.2 문제 2: 문자열에서 특정 문자 개수 세기
`count()` 메소드를 사용하여 특정 문자가 문자열에 몇 번 등장하는지 셀 수 있습니다.

```python
word = "banana"
count_a = word.count('a')  # 'a'가 몇 번 나오는지 세기
print(count_a)  # 3
```

.

### 1.1.2 연산자

#### 1.1.2.1 산술 연산자

| 연산자 | 설명 | 예제 |
|--------|------|------|
| `+` | 덧셈 | `5 + 3` → `8` |
| `-` | 뺄셈 | `5 - 3` → `2` |
| `*` | 곱셈 | `5 * 3` → `15` |
| `/` | 나눗셈 | `5 / 3` → `1.666...` |
| `//` | 몫 | `5 // 3` → `1` |
| `%` | 나머지 | `5 % 3` → `2` |
| `**` | 거듭제곱 | `5 ** 3` → `125` |

#### 1.1.2.2 비교 연산자

| 연산자 | 설명 | 예제 |
|--------|------|------|
| `==` | 같음 비교 | `5 == 3` → `False` |
| `!=` | 다름 비교 | `5 != 3` → `True` |
| `>` | 초과 비교 | `5 > 3` → `True` |
| `<` | 미만 비교 | `5 < 3` → `False` |
| `>=` | 이상 비교 | `5 >= 3` → `True` |
| `<=` | 이하 비교 | `5 <= 3` → `False` |

#### 1.1.2.3 논리 연산자

| 연산자 | 설명 | 예제 |
|--------|------|------|
| `and` | 논리 AND | `True and False` → `False` |
| `or` | 논리 OR | `True or False` → `True` |
| `not` | 논리 NOT | `not True` → `False` |

#### 예제 코드

```python
print(5 + 3)  # 덧셈
print(5 - 3)  # 뺄셈
print(5 * 3)  # 곱셈
print(5 / 3)  # 나눗셈
print(5 // 3) # 몫
print(5 % 3)  # 나머지
print(5 ** 3) # 거듭제곱
```

#### 비교 연산자 및 논리 연산자

```python
print(5 > 3)  # True
print(5 < 3)  # False
print(5 == 3) # False
print(5 != 3) # True

print(True and False)  # False
print(True or False)   # True
print(not True)        # False
```



### 1.1.3 변수

#### 1.1.3.1 변수란?
변수(Variable)는 데이터를 저장하는 공간이며, 파이썬에서는 값을 할당하면 자동으로 변수의 타입이 결정된다.

#### 1.1.3.2 변수 선언 및 할당
```python
a = 10        # 정수형 변수
b = 3.14      # 실수형 변수
c = "Hello"   # 문자열 변수
d = True      # 불리언 변수
```

#### 1.1.3.3 변수 명명 규칙
- 영문자(A-Z, a-z), 숫자(0-9), 밑줄(_)을 사용할 수 있음
- 숫자로 시작할 수 없음
- 공백을 포함할 수 없음
- 대소문자를 구별함
- 파이썬의 예약어(keyword)는 사용할 수 없음 (예: `class`, `def`, `import` 등)

#### 1.1.3.4 다중 할당
```python
x, y, z = 1, 2, 3  # 여러 변수에 한 번에 값 할당
print(x, y, z)     # 출력: 1 2 3
```

#### 1.1.3.5 변수 사용 시 유의할 점
* **내장 함수 및 클래스명을 변수명으로 사용하지 않기**
   ```python
   sum = 10  # sum() 함수가 아닌 변수로 정의됨
   print(sum([1, 2, 3]))  # 오류 발생
   ```
   - `sum`, `len`, `max`, `min` 등의 내장 함수명을 변수명으로 사용하면 기존 함수 기능이 사라짐
   - 해결 방법: `del sum`을 사용하여 기존 변수를 삭제 후 다시 사용

* **변수명은 가독성 있게 작성하기**
   ```python
   a = 100  # 의미 없는 변수명
   student_score = 100  # 의미 있는 변수명
   ```
   - 코드의 가독성을 위해 의미 있는 변수명을 사용하는 것이 좋음

* **전역 변수와 지역 변수의 차이 이해하기**
   ```python
   def func():
       x = 20  # 지역 변수
       print(x)

   x = 10  # 전역 변수
   func()  # 20 출력
   print(x)  # 10 출력
   ```
   - 함수 내부에서 선언된 변수는 지역 변수이며, 함수 밖의 변수와 다르게 동작함

## 1.2 입출력

### 1.2.1 `print()` 함수

`print()`는 문자열, 변수, 연산의 결과를 표준출력장치인 화면에 출력하는 함수이다.
* 출력하기 위해서는 출력하고자 하는 내용을 print() 함수의 괄호안에 넣는다.
* print() 괄호 안에 아무런 내용없다면 한 줄 공백을 출력한다.
* print() 함수는 줄바꿈(\n) 기능이 포함되어 있다.

* 기본 사용법
```python
print("Hello, World!")  # Hello, World!
```

* 여러 값 출력
```python
print("Hello", "Python", 2024)  # Hello Python 2024
```

* `sep` 옵션 (구분자 지정)
```python
print("Hello", "Python", sep=" - ")  # Hello - Python
```

* `end` 옵션 (출력 끝 문자 지정)
```python
print("Hello", end=" ")
print("Python")  # Hello Python (줄바꿈 없이 출력)
```

* `format()` 함수 사용
```python
print("{}님, {}원이 입금되었습니다.".format("홍길동", 5000))
```

* f-string 사용
```python
name = "홍길동"
money = 5000
print(f"{name}님, {money}원이 입금되었습니다.")
```

* 출력 대상 지정 (`file` 옵션)
```python
with open("output.txt", "w") as f:
    print("Hello, File!", file=f)  # 파일에 저장됨
```



### 1.2.2  `input()` 함수
`input()` 함수는 프로그램 실행 중에 표준입력장치인 키보드로부터 데이터를 입력받는 함수이다. 입력 받은 데이터는 변수에 저장하여 사용한다.

* 기본 사용법
  ```python
  name = input("이름을 입력하세요: ")
  print("안녕하세요,", name)
```

* 입력값을 숫자로 변환
`input()` 함수는 기본적으로 문자열(str)로 입력을 받으므로, 숫자로 변환하려면 `int()` 또는 `float()` 함수를 사용해야 한다.

  ```python
  age = int(input("나이를 입력하세요: "))
  print("내년 나이는", age + 1, "살입니다.")
  ```

* 여러 값 입력 받기
`split()` 함수를 이용하면 한 번에 여러 값을 입력받을 수 있다.

  ```python
  x, y = input("두 개의 숫자를 입력하세요: ").split()
  x = int(x)
  y = int(y)
  print("두 수의 합:", x + y)
  ```

*  map()을 활용한 입력 변환
`map()` 함수를 사용하면 여러 값을 한 번에 원하는 타입으로 변환할 수 있다.

  ```python
  n = list(map(int, input("공백으로 구분된 숫자들을 입력하세요: ").split()))
  print("입력된 숫자 리스트:", n)
  ```

* 표현식 평가(Expression Evaluation)
  * eval() 함수  
  `eval()` 함수는 문자열로 표현된 파이썬 표현식을 실행하는 함수이다.

    ```python
    expr = input("계산식을 입력하세요: ")
    result = eval(expr)
    print("결과:", result)
    ```

    ⚠️ `eval()`은 단순한 숫자 연산부터 함수 호출, 객체 생성, 심지어 파일 삭제 같은 위험한 작업까지 수행할 수 있으므로 보안상 위험이 있을 수 있다.

  * ast.literal_eval() 함수   
  `ast.literal_eval()` 함수는 문자열을 안전하게 파싱하여 리터럴(literal) 값으로 변환하는 함수이다. 즉, 숫자, 문자열, 리스트, 딕셔너리, 튜플 등 안전한 기본 자료형만 허용하고, 함수 호출이나 객체 생성을 차단한다.

    ```python
    import ast
    expr = input("리스트를 입력하세요: ")
    parsed_expr = ast.literal_eval(expr)
    print("변환된 리스트:", parsed_expr)
    ```




## 5. 마무리 및 실습 문제

### 5.1 실습 문제

1. 사용자로부터 숫자 두 개를 입력받아 덧셈, 뺄셈, 곱셈, 나눗셈을 수행하는 프로그램을 작성하세요.
2. 문자열로 입력된 리스트(예: `"[1, 2, 3, 4]"`)를 `ast.literal_eval()`을 이용해 리스트로 변환하고, 그 합을 출력하세요.
3. 사용자가 입력한 식을 `eval()`로 계산해 출력하는 프로그램을 작성하세요. (주의: 보안 위험 설명)
4. 여러 개의 변수를 한 줄로 입력받고 이를 분리하여 출력하는 프로그램을 작성하세요.
5. 사용자로부터 입력받은 문자열을 뒤집어서 출력하는 프로그램을 작성하세요.

### 5.2 정리

- 기본자료형, 연산자, 변수 개념을 익혔다.
- 입력과 출력을 활용할 수 있다.
- `eval()`과 `ast.literal_eval()`을 이해하고 활용할 수 있다.
- 포맷팅된 출력을 사용할 수 있다.




```python
!jupyter

```

    usage: jupyter [-h] [--version] [--config-dir] [--data-dir] [--runtime-dir] [--paths] [--json]
                   [--debug]
                   [subcommand]
    
    Jupyter: Interactive Computing
    
    positional arguments:
      subcommand     the subcommand to launch
    
    options:
      -h, --help     show this help message and exit
      --version      show the versions of core jupyter packages and exit
      --config-dir   show Jupyter config dir
      --data-dir     show Jupyter data dir
      --runtime-dir  show Jupyter runtime dir
      --paths        show all Jupyter paths. Add --json for machine-readable format.
      --json         output paths as machine-readable json
      --debug        output debug information about paths
    
    Available subcommands: bundlerextension console dejavu execute kernel kernelspec migrate nbclassic
    nbconvert nbextension notebook run server serverextension troubleshoot trust
    
    Please specify a subcommand or one of the optional arguments.

