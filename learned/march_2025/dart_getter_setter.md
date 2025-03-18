# Dart getter, setter
     
     
      
`property` `setter` 를 연습해보고 싶어서 작성했습니다.
     
     
https://dart.dev/language/methods : Dart 공식 문서 `Getter and Setter`
    
    
### Getters and setters are special methods that provide read and write access to an object's properties. Recall that each instance variable has an implicit getter, plus a setter if appropriate. You can create additional properties by implementing getters and setters, using the `get` and `set` keywords:
    
    
- 게터와 세터는 객체의 프로퍼티에 대한 읽기 및 쓰기 액세스를 제공하는 특수 메서드입니다. 각 인스턴스 변수에는 암시적 게터와 적절한 경우 설정자가 있다는 것을 기억하세요. get 및 set 키워드를 사용하여 게터와 세터를 구현하여 추가 프로퍼티를 만들 수 있습니다:
     
     
- 게터 객체의 프로퍼티에 대한 읽기 액세스를 제공하는 특수 메서드
- 세터 객체의 프로퍼티에 대한 쓰기 액세스를 제공하는 특수 메서드
      
     
저는 `gettter` , `setter` 를 사용하는 이유는
     
클라이언트 상에 데이터를 개인정보 보호 및 데이터 보안 위해 사용하는게 아닌가? 생각합니다.
     
      
`getter` 사용방법
      
      
     
```dart
Class _Dog {}

class Dog {
  String _address;

  Dog(this._address);

  String get address => _address; // get 읽기 가능, getter

  String get address {  // getter
    return _address;
  }
}
```
     
     
     
- getter 는 `class` or 맴버 변수 앞에 `_` (private) 작성하며, `get` 으로 읽기가 가능합니다.
    
    
    
`setter` 사용방법
     
     
     
```dart
class Dog {
  String name;
  String _address;

  Dog(this.name, this._address);

  String get address => _address;

  set address(String value) { // set 쓰기 가능
      print('$name의 주소는 $address입니다.');
    }
  }
}
```
     
    
     
- `get` 을 사용하면  `set` 사용이 가능합니다.
    
    
## Public

```dart
void main() {
  Dog jinDo = Dog(name: '진도', address: '서울 용산구 **동');
  print(jinDo.name);  // 진도
  print(jinDo.address);  // 서울 용산구 **동
  jinDo.dogInFo(); // 진도의 주소는 서울 용산구 **동입니다.
}

class Dog {
  String name;
  String address;

  Dog({required this.name, required this.address});

  void dogInFo() {
    print('$name의 주소는 $address입니다.');
  }
}
```
    
     
이 코드를 Private로 한번 연습해 볼려고 합니다.
    
     
## Private

```dart
class Dog {
  String name;
  String _address;

  Dog({required this.name, required this._address});
}

Named parameters can't start with an underscore. (Documentation)
```

img width="537" alt="Image" src="https://github.com/user-attachments/assets/78d3db89-2edb-43ff-a7bf-7562f90bdb72" />

https://dart.dev/tools/diagnostic-messages?utm_source=dartdev&utm_medium=redir&utm_id=diagcode&utm_content=private_optional_parameter#private_optional_parameter

**private_optional_parameter**

*Named parameters can't start with an underscore.*

→ 그렇다면 `Positinal parameter` 로 작성하고

```dart
class Dog {
  String name;
  String _address;

  Dog(this.name, this._address);

  String get address => _address;

  void set address(String value) {
    print('$name의 주소는 $address입니다.');
  }
}

Unnecessary return type on a setter. (Documentation)
setter 에 불필요한 리턴 유형이 있습니다
```

<img width="512" alt="Image" src="https://github.com/user-attachments/assets/baf0593a-a8ad-4a35-b428-5f6e4f3d5d10" />

https://dart.dev/tools/diagnostic-messages?utm_source=dartdev&utm_medium=redir&utm_id=diagcode&utm_content=private_optional_parameter#private_optional_parameter

**avoid_return_types_on_setters**

```bash
Description

The analyzer produces this diagnostic when a setter has an explicit return type.
Setters never return a value, so declaring the return type of one is redundant.
```

오류는 아니지만 확인해보니 `setter` 는 **값을 설정하는 역할** 만 하며, 반환값을 가지지 않습니다.

반환 타입을 명시 할 필요없고, 중복이라는 의미

→ 즉 `void` 도 값을 반환하지 않으니, 중복이라는 의미란 말 같습니다.

```bash
void main() {
  Dog jinDo = Dog('진도','서울 용산구 **동');
  jinDo.name;
  jinDo.address;
  jinDo._address;
}
```

<img width="385" alt="Image" src="https://github.com/user-attachments/assets/b9996996-db99-4419-8e1b-5d30769f3991" />

```bash
여기서 jinDo.address; address 가 property 이므로 p

jinDo._address; _address 는 Field, 즉 속성(맴버 변수)을 의미하여 f 로 나옵니다.
```

```dart
void main() {
  Dog jinDo = Dog('진도','서울 용산구 **동');
  jinDo.address(); // Error
}

The expression doesn't evaluate to a function, so it can't be invoked. (Documentation)
표현식이 함수로 평가되지 않으므로 호출할 수 없습니다. (문서)
```

저는 ‘jinDo.address’가 `set mathod` , `setter` 일 줄 알고 호출 했는데
확인해보니 `getter` 였습니다.

<img width="435" alt="Image" src="https://github.com/user-attachments/assets/9f2aefbf-bcec-4243-a8a7-1d118392dd7e" />

`setter` 값을 할당해야 호출하는 문법…

```dart
void main() {
  Dog jinDo = Dog('진도','서울 용산구 **동');
	jinDo.address = ''; // setter 호출
}
```

<img width="408" alt="Image" src="https://github.com/user-attachments/assets/8d3d18fd-b4e2-4c34-aa1a-4df22b8d6747" />

그리고 `set method` 에 조건문 도 확인 할 수 있었습니다. 

```dart
class Dog {
  String name;
  String _address;

  Dog(this.name, this._address);

  String get address => _address;

  set address(String value) {
    if (value.length < 5 || value.isEmpty) {
      print('주소를 입력해주세요');
    } else {
      print('$name의 주소는 $address입니다.');
    }
  }
}
```

# 최종 코드

```dart
void main() {
  Dog jinDo = Dog('진도', '서울 용산구 **동');
  print(jinDo.address); // getter
  jinDo.address = '';  // setter
}

class Dog {
  String name;
  String _address;

  Dog(this.name, this._address);

  String get address => _address;

  set address(String value) {
    if (value.length < 5 || value.isEmpty) {
      print('주소를 입력해주세요');
    } else {
      print('$name의 주소는 $address입니다.');
    }
  }
}

```

