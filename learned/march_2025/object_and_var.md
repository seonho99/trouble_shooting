수업 중 궁금한 내용이 생겼습니다.



`Object` 와 `var` 내용을 설명해주시는데

제가 알았던 두 사이의 개념이 헷갈려서 찾아보게 되었습니다.



### `Object` , `var`  공통점 & 차이점



| Object | var |
| --- | --- |
| 👉 컴파일러에서 변수 타입 지정함 | 👉 컴파일러에서 변수 타입 지정함 |
| 👉 모든 타입의 변수 값을 담을 수 있음 | 👉 모든 타입의 변수 값을 담을 수 있음 |
| 👉 Object 타입은 명시적으로 타입 지정 | 👉 타입을 명시하지 않고 변수를 선언할 때 사용되는 키워드 |
| 👉 Object 는 모든 타입의 기본 타입 역할 |  |



저는 자바 스터디를 2달 했었고, 자바에서 `Object` 는 최상위 부모 클래스로

`Object` 타입 변수는 **자바의 모든 객체를 참조 할 수 있다** 알고 있었고

`Dart`에서도 동일한 역할을 하는 것으로 알고 있습니다.



헷갈렸던 부분이 `Object` 와 `var` 는 컴파일러에서 변수 타입을 지정하고 둘의 타입은 다르닌깐

같은 변수명을 사용해도 동작하지 않을까? 라는 생각이 들었습니다.



<img width="433" alt="Image" src="https://github.com/user-attachments/assets/6f27c54f-dc76-452e-8798-f8d86b4c73d8" />



```dart
void main() {
	Object x;
	var x;
}

ERROR : The name 'x' is already defined.
```



선생님께서 `Dart` 는 **문법적으로 같은 변수를 사용할 수 없다.** 말씀해주셨고,



<img width="619" alt="Image" src="https://github.com/user-attachments/assets/c270f092-665a-4288-8f2b-2af2d8b469ed" />



자바에서 같은 변수를 사용할 수 있다 라는 생각에 궁금해서 코드 작성해보니,

**자바도 같은 변수를 사용하지 못하며**, 알고보니 파이썬에서 타입 없이 같은 변수를 사용 했었습니다;;



```java
public class Main {
    public static void main(String[] args) {
    
    int num1 = 10;
    int num2 = 10;
    
    Integer obj1 = new Integer(10);
    Integer obj2 = new Integer(10);
    
    System.out.println("obj1: " + System.identityHashCode(obj1));
    System.out.println("obj2: " + System.identityHashCode(obj2));            
    System.out.println(obj1 == obj2);
    }
}

변수의 값은 동일하나 객체 주소가 다르다는 내용을 머리에 담고 있었습니다.
```



`Dart, 자바`  **문법적으로 같은 변수를 사용 못하는 내용** 을 알았습니다.



<img width="412" alt="Image" src="https://github.com/user-attachments/assets/98e470db-0196-4914-aee7-2076756bf479" />



<img width="543" alt="Image" src="https://github.com/user-attachments/assets/77e981c9-44b2-4447-9a58-947a0b9c9068" />



`Dart` 에서 메모리 인스턴스 주소를 참조 하는데 `identical()` 사용하며,

두 이미지는 `runtimeType` 을 적용 했을 때, 안 했을때 차이는 뭘까?

### 제 생각은



👉  컴파일 전 두 인스턴스는 서로 다른 메모리 주소를 사용하고 있어

`identical()` 에선 `false` 가 나오다고 생각이 들고,



👉 runtime 후에는 `Different` 클래스 타입으로,
두 인스턴스 타입은 동일하므로 `true` 가 반환 된다.

→ 머리에 담았습니다.



<img width="561" alt="Image" src="https://github.com/user-attachments/assets/cb2b44fa-20a7-46fb-b12a-3a2eaf6184b3" />



자습시간에 선생님께 `Object` 를 질문 드렸고

문주현 선생님께 코드 및 설명을 받았습니다.



<img width="701" alt="Image" src="https://github.com/user-attachments/assets/f198ffb1-72b2-4289-9c80-4a2066da6665" /> 



```dart
void main() {
  Object o = "sss";
  var o1 = "sss";
  String s = "sss";
  
  print(s.length); // String s의 길이 3
  print(s.runtimeType); // runtime String 

  print(o1.length); // var o1의 길이 3
  print(o1.runtimeType); // runtime String
  
  // print(o.length); // 에러
  print(o.runtimeType); // 코드는 Object, runtime String
}
```



<img width="695" alt="Image" src="https://github.com/user-attachments/assets/f764821f-33d1-49bb-9587-4656463c0434" />



<img width="690" alt="Image" src="https://github.com/user-attachments/assets/ff4dcb3a-7029-435a-820f-888935092c9a" />



<img width="909" alt="Image" src="https://github.com/user-attachments/assets/f7155922-a709-4428-ad27-864fa336344b" />



이미지 들을 보고 `Object` 와 `var` 를 차이점을 좀 더 알게 되었습니다.



| **Object** | **var** |
| --- | --- |
| 코드를 실행하기 전 **타입변환 X**  | 코드를 실행하기 전 **타입변환 O** |
| **타입만 정의 인스턴스 X** | **타입만 정의 인스턴스 O** |
→ **인스턴스 메모리 참조 주소 X** | → **인스턴스 메모리 참조 주소 O** |
| 인스턴스 X, length X | 인스턴스 O, length O |



## 결과적



`Object` 는 최상위 타입으로  타입만 명시하며 `instance` 주소를 참조 할 수 없다!

그리고 `Object` 는  `Flutter Widget` 도 포함 한다는 사실도 알게 되었습니다!
