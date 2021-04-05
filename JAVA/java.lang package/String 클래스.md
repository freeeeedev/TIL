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

* '+' 연산자를 이용해서 문자열을 결합하는 경우 인스턴스 내의 문자열이 바뀌는 것이 아니라  
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

* 이처럼 덧셈 연산자 '+'를 사용해서 문자열을 결합하는 것은 매 연산 시마다 새로운 문자열을 가진  
  String 인스턴스가 생성되어 메모리 공간을 차지하게 되므로 가능한 결합횟수를 줄이는 것이 좋다.
  
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

* 생성자를 이용한 경우에는 new 연산자에 의해서 메모리 할당이 이루어지기 때문에 항상 새로운 String 인스턴스가 생성된다.  
  그러나 문자열 리터럴은 이미 존재하는 것을 재사용한다. (문자열 리터럴은 클래스가 메모리에 로드될 때 자동적으로 미리 생성된다.)

![9-1](../images/9-1.png)

```java
class Example {
    public static void main(String[] args) {
        String str1 = "abc";
        String str2 = "abc";

        System.out.println(str1 == str2);
        System.out.println(str1.equals(str2));

        String str3 = new String("abc");
        String str4 = new String("abc");

        System.out.println(str3 == str4);
        System.out.println(str3.equals(str4));
    }
}
```

```
true
true
false
true
```

* equals()를 사용했을 때는 문자열의 내용을 비교하기 때문에 두 경우 모두 true를 결과로 얻는다.  
  하지만, 각 String 인스턴스의 주소를 '=='로 비교했을 때는 결과가 다르다.

## 문자열 리터럴

* 자바 소스파일에 포함된 모든 문자열 리터럴은 컴파일 시에 클래스 파일에 저장된다.

* 이 때 같은 내용의 문자열 리터럴은 한 번만 저장된다.  
  문자열 리터럴도 String 인스턴스이고, 한 번 생성하면 내용을 변경할 수 없으니 하나의 인스턴스를 공유하면 되기 때문이다.

* 클래스 파일에는 소스파일에 포함된 모든 리터럴의 목록이 있다.

* 해당 클래스 파일이 클래스 로더에 의해 메모리에 올라갈 때, 이 리터럴의 목록에 있는 리터럴들이 JVM 내에 있는  
  '상수 저장소(constant pool)'에 저장된다. 이 때, 이곳에 "AAA"와 같은 문자열 리터럴이 자동적으로 생성되어 저장되는 것이다.

## 빈 문자열(empty string)

* char형 배열도 길이가 0인 배열을 생성할 수 있고, 이 배열을 내부적으로 가지고 있는 문자열이 바로 빈 문자열이다.  
  `String s = "";`과 같은 문장이 있을 때, s가 참조하고 있는 String 인스턴스는 내부에 길이가 0인 char형 배열을 저장하고 있다.

* `String s = "";`과 같은 표현이 가능하다고 해서 `char c = '';`와 같은 표현도 가능한 것은 아니다.  
  char형 변수에는 반드시 하나의 문자를 지정해야한다.

* **C 언어에서는 문자열의 끝에 널 문자가 항상 붙지만, 자바에서는 사용하지 않는다. 대신 문자열의 길이정보를 따로 저장한다.**

```java
String s = "";  // 빈 문자열로 초기화
char c = ' ';   // 공백으로 초기화 
```

* 일반적으로 변수를 선언할 때, 각 타입의 기본값으로 초기화 하지만 String은 참조형 타입의 기본값인 null보다는 빈 문자열로,  
  char형은 기본값인 '\u0000' 대신 공백으로 초기화 하는 것이 보통이다.
  
```java
class Example {
    public static void main(String[] args) {
        char[] arr = new char[0];
        String str = new String(arr);

        System.out.println(arr.length);
        System.out.println(str.length());
    }
}
```

```
0
0
```

## String 클래스의 생성자와 메소드

## join()과 StringJoiner

## 유니코드의 보충문자

## 문자 인코딩 변환

## String.format()

## 기본형 값을 String으로 변환

## String을 기본형 값으로 변환

# 참고
