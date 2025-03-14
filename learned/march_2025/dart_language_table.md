# Dart 언어에서 객체와 인스턴스 변수 정리





- 객체 : **현실에서의 실체**를 지칭합니다.



- 인스턴스 : 가상 환경에서 **class의 구체적인 실체**를 지칭합니다.



```dart
void main() {
  Person p1 = Person(30);  // 인스턴스 Person
  Person p2 = Person(25);  // 인스턴스 Person
}
```

- 인스턴스 변수 or 맴버 변수



```dart
class Person {
  int age;  // 인스턴스 변수 or 맴버 변수 : 클래스의 속성

  Person(this.age);
}
```



- 클래스의 인스턴스

```dart

void main() {
	Person p1 = Person(30);  // Person 클래스의 인스턴스 p1
  Person p2 = Person(25);  // Person 클래스의 인스턴스 p2
}

class Person {
  int age;

  Person(this.age);
}
```