# String 클래스

* 기존의 다른 언어에서는 문자열을 char형의 배열로 다루었으나 자바에서는 문자열을 위한 String 클래스를 제공한다.  
  String 클래스는 문자열을 저장하고 이를 다루는데 필요한 메소드를 함께 제공한다.

## 변경 불가능한(immutable) 클래스

* String 클래스에는 문자열을 저장하기 위해서 문자형 배열 참조변수 value를 인스턴스 변수로 정의해놓고 있다.  
  인스턴스 생성 시 생성자의 매개변수로 입력받는 문자열은 이 인스턴스 변수(value)에 문자형 배열(char[])로 저장되는 것이다.

```java
public final class String implements java.io.Serializable, Comparable<String>, CharSequence {
    private final char value[];
    ...
}
```

* 한번 생성된 String 인스턴스가 갖고 있는 문자열은 읽어 올 수만 있고, 변경할 수는 없다.

* 아래의 코드와 같이 '+' 연산자를 이용해서 문자열을 결합하는 경우 인스턴스 내의 문자열이 바뀌는 것이 아니라  
  새로운 문자열("ab")이 담긴 String 인스턴스가 생성되는 것이다.
  
```java
class Example {
    public static void main(String[] args) {
        String a = "a";
        String b = "b";

        System.out.println(a);
        System.out.println(System.identityHashCode(a));
        System.out.println(System.identityHashCode(b));

        a = a + b;

        System.out.println(a);
        System.out.println(System.identityHashCode(a));
        System.out.println(System.identityHashCode(b));
    }
}
```

```
a
1404928347
604107971
ab
123961122
604107971
```

* 이처럼 덧셈 연산자 '+'를 사용해서 문자열을 결합하는 것은 매 연산 시마다  
  새로운 문자열을 가진 String 인스턴스가 생성되어 메모리 공간을 차지하게 되므로 가능한 결합횟수를 줄이는 것이 좋다.
  
* 문자열간의 결합이나 추출 등 문자열을 다루는 작업이 많이 필요한 경우에는 StringBuffer 클래스를 사용하는 것이 좋다.  
  StringBuffer 인스턴스에 저장된 문자열은 변경이 가능하므로 하나의 StringBuffer 인스턴스만으로도 문자열을 다루는 것이 가능하다.

## 문자열의 비교

* 문자열을 만들 때는 두 가지 방법, 문자열 리터럴을 지정하는 방법과 String 클래스의 생성자를 사용해서 만드는 방법이 있다.

```java
String str1 = "abc";              // 문자열 리터럴 "abc"의 주소가 str1에 저장됨.
String str2 = "abc";              // 문자열 리터럴 "abc"의 주소가 str2에 저장됨.
String str3 = new String("abc");  // 새로운 String 인스턴스 생성
String str4 = new String("abc");  // 새로운 String 인스턴스 생성
```

* String 클래스의 생성자를 이용한 경우에는 new 연산자에 의해서 메모리 할당이 이루어지기 때문에 항상 새로운 String 인스턴스가 생성된다.    
  그러나 문자열 리터럴은 이미 존재하는 것을 재사용하는 것이다. (문자열 리터럴은 클래스가 메모리에 로드될 때 자동적으로 미리 생성된다.)

## 문자열 리터럴

## 빈 문자열(empty string)

## String 클래스의 생성자와 메소드

## join()과 StringJoiner

## 유니코드의 보충문자

## 문자 인코딩 변환

## String.format()

## 기본형 값을 String으로 변환

## String을 기본형 값으로 변환

# 참고
