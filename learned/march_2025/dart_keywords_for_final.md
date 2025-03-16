# Dart에서 `final` 키워드 정리

코드를 보면서 헷갈렸던 `final` 부분을 정리하고 작성합니다.

`final` 이란?

- A final variable can be set only once;

→ `final` 변수는 한 번만 설정할 수 있다.

Here's an example of creating and setting a `final` variable:

```dart
final name = 'Bob'; // Without a type annotation
final String nickname = 'Bobby';
```

You can't change the value of a `final` variable:

```dart
✗ static analysis: failure
name = 'Alice'; // Error: a final variable can only be set once.
```

출처 : https://dart.dev/language/variables 공식문서 중 `final`

공식 문서을 보고

저는 ‘`final` 은 변수의 값을 한 번만 설정 해 주는구나’ 생각했습니다.

# 코드 1.

여기서 doJi 의 값은 10 or 20 중 어떤 것일까요?

```dart
void main() {
  final jinDo = Dog(10);
  final doJi = jinDo;

  jinDo.age = 20;

  print(doJi.age);
}

class Dog {
  int age;

  Dog(this.age);
}
```

👉 정답은 20 입니다.

<img width="698" alt="Image" src="https://github.com/user-attachments/assets/a13d3b98-31a2-4768-9a07-b1278d912dac" />

```dart
void main() {
  final jinDo = Dog();
  final doJi = jinDo;

  doJi.age = 20; // error
'age' can't be used as a setter because it's final. (Documentation)

  print(doJi.age); // 출력 X
}

class Dog {
  final int age = 10;
}
```

10을 생각하셨던 분들은 저와 마찬가지로 이런 코드와 착각하지 않았을까? 생각합니다.

**class에 instance 변수 값** 을 10 으로 지정해야 값이 변하지 않습니다.

<img width="692" alt="Image" src="https://github.com/user-attachments/assets/c389895d-6207-4385-bdbc-ab884abc8003" />

# 코드 2.

그렇다면 poMe 의 값은 10 or 20 중 어떤 것일까요?

```dart
void main() {
  final jinDo = Dog(10);
  final doJi = jinDo;
  final poMe = Dog(10);

  jinDo.age = 20;

  print(jinDo.age);
  print(doJi.age);
  print(poMe.age);
}

class Dog {
  int age;

  Dog(this.age);
}

```

👉 정답은 10 입니다.

왜 코드 1. 처럼 poMe는 왜 20이 아니지?

```dart
final jinDo = Dog(10);
final doJi = jinDo;

final poMe = Dog(10);
```

jinDo 와 doJi 는 같은 `instance` 를 바라보고 있습니다.

poMe 는 `instance` 명이 같은 Dog(10) 여도,

`instance` 주소 참조 값이 다릅니다.

```dart
void main() {
  final jinDo = Dog(10);
  final doJi = jinDo;
  final poMe = Dog(10);

  jinDo.age = 20;

  print(jinDo.age);  // 20
  print(doJi.age);   // 20
  
  print(poMe.age);   // 10
  
  print(jinDo == doJi); // true
  print(identical(jinDo, doJi));  // true
  
  print(jinDo == poMe);  // false
  print(identical(jinDo, poMe));  // false
}

class Dog {
  int age;

  Dog(this.age);
}

```



 <img width="692" alt="Image" src="https://github.com/user-attachments/assets/dd46166d-91c4-4c5f-a263-eb790f7c2228" />

<img width="600" alt="Image" src="https://github.com/user-attachments/assets/6e0c8d83-74fc-4c2c-87ba-b96333a53e5c" />

이미지처럼 jinDo 와 doJi 는 같은 `instance` 를 참조하고 있고,

`jinDo.age = 20;` 시 두 `instance` 는  같은 `instance` 를 참조하기 때문에

두 `instance 변수` 값이 20 으로 변경 되는 것입니다.

### → Dart 에서 같은 `instance` 참조하면 `instance 변수` 명이 다르더라도, 두 변수는 같은 메모리 주소를 가리키게 됩니다.

### 그리고 `final` 은 언제 사용이 될까? 하는 생각이 들었습니다.

1. `final` 은 런타임에서 실행된다.

→ 즉 앱이 실행될 때 사용된다. 앱 실행 중에 값이 설정되고,

한번 할당된 값은 이후 변경할 수 없습니다.

1. `final` 변수는 한 번만 설정할 수 있다.

→ DB 에 변수 값이 들어갈 때 정확히 한 번만 값을 할당해야 해서, 이 목적으로 사용된다.

저는 `final` 을 이런 목적에 사용하지 않을까? 생각합니다.