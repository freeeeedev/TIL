# Object 클래스

## equals(Object obj)

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

* 매개변수로 객체를 받아서 자신과 비교하여 그 결과를 boolean 값으로 알려 주는 역할을 한다.

* 위의 코드에서 알 수 있듯이 두 객체의 같고 다름을 참조변수의 값(객체의 주소값)으로 판단하기 때문에,  
  서로 다른 두 객체를 equals 메소드로 비교하면 항상 false를 결과로 얻게 된다.

* 객체를 생성할 때, 메모리의 비어있는 공간을 찾아 생성하므로 서로 다른 두 객체가 같은 주소를 갖는 일은 없다.

```java
class Person {
    long id;

    public boolean equals(Object obj) {
        if(obj instanceof Person)
            return id == ((Person)obj).id;
        else
            return false;
    }

    Person(long id) {
        this.id = id;
    }
}

public class Example {
    public static void main(String[] args) {
        Person p1 = new Person(8011081111222L);
        Person p2 = new Person(8011081111222L);

        if(p1 == p2)
            System.out.println("p1과 p2는 같은 사람입니다.");
        else
            System.out.println("p1과 p2는 다른 사람입니다.");

        if(p1.equals(p2))
            System.out.println("p1과 p2는 같은 사람입니다.");
        else
            System.out.println("p1과 p2는 다른 사람입니다.");
    }
}
```

```java
class Person {
    long id;

    public boolean equals(Object obj) {
        return obj instanceof Person && id == ((Person)obj).id;
    }

    Person(long id) {
        this.id = id;
    }
}

public class Example {
    public static void main(String[] args) {
        Person p1 = new Person(8011081111222L);
        Person p2 = new Person(8011081111222L);

        println(p1 == p2 ? "같은 사람" : "다른 사람");
        println(p1.equals(p2) ? "같은 사람" : "다른 사람");
    }

    static void println(String str) {
        System.out.println("p1과 p2는 " + str + "입니다.");
    }
}
```

```
p1과 p2는 다른 사람입니다.
p1과 p2는 같은 사람입니다.
```

* equals 메소드가 Person 인스턴스의 주소값이 아닌 멤버변수 id 값을 비교하도록 하기위해 다음과 같이 오버라이딩 했다.

* String 클래스 역시 오버라이딩을 통해서 String 인스턴스가 갖는 문자열 값을 비교하도록 되어있다.  
  그렇기 때문에 같은 내용의 문자열을 갖는 두 String 인스턴스에 equals 메소드를 사용하면 true 값을 얻는 것이다.
  
* Date, File, Wrapper 클래스(Integer, Double 등)의 equals 메소드도 주소값이 아닌 내용을 비교하도록 오버라이딩되어 있다.  
  그러나 의외로 StringBuffer 클래스는 오버라이딩되어 있지 않다.

## hashCode()

```java
public native int hashCode();
```

* 이 메소드는 해싱(hashing)기법에 사용되는 '해시함수(hash function)'를 구현한 것이다.  
  해시함수는 찾고자하는 값을 입력하면, 그 값이 저장된 위치를 알려주는 해시코드(hashcode)를 반환한다.

* Object 클래스에 정의된 hashCode 메소드는 객체의 주소값으로 해시코드를 만들어 반환한다. 따라서,  
  32bit JVM에서는 4 byte 주소값으로 해시코드(4 byte)를 만들기 때문에 서로 다른 두 객체는 결코 같은 해시코드를 가질 수 없었지만,  
  64bit JVM에서는 8 byte 주소값으로 해시코드(4 byte)를 만들기 때문에 해시코드가 중복될 수 있다.
  
* 클래스의 인스턴스 변수 값으로 객체의 같고 다름을 판단해야하는 경우라면 equals 메소드 뿐만 아니라 hashCode 메소드도  
  적절히 오버라이딩해야 한다. 같은 객체라면 hashCode 메소드를 호출했을 때의 결과값인 해시코드도 같아야 하기 때문이다.
  
* 해싱기법을 사용하는 HashMap이나 HashSet과 같은 클래스에 저장할 객체라면 반드시 hashCode 메소드를 오버라이딩해야 한다.

```java
public class Example {
    public static void main(String[] args) {
        String str1 = new String("abc");
        String str2 = new String("abc");

        System.out.println(str1.equals(str2));

        System.out.println(str1.hashCode());
        System.out.println(str2.hashCode());

        System.out.println(System.identityHashCode(str1));
        System.out.println(System.identityHashCode(str2));
    }
}
```

```
true
96354
96354
1404928347
604107971
```

* String 클래스는 문자열의 내용이 같으면, 동일한 해시코드를 반환하도록 hashCode 메소드가 오버라이딩되어 있기 때문에,  
  문자열의 내용이 같은 str1과 str2에 대해 hashCode() 메소드를 호출하면 항상 동일한 해시코드값을 얻는다.
  
* `System.identityHashCode(Object x)`는 Object 클래스의 hashCode 메소드처럼 객체의 주소값으로 해시코드를 생성하기 때문에 모든  
  객체에 대해 항상 다른 해시코드값을 반환할 것을 보장한다. 그래서 str1와 str2가 해시코드는 같지만 서로 다른 객체라는 것을 알 수 있다.
  
* `System.identityHashCode(Object x)`의 호출결과는 실행 할 때마다 달라질 수 있다.

## toString()

```java
public String toString() {
    return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

* 이 메소드는 인스턴스에 대한 정보를 문자열(String)로 제공할 목적으로 정의한 것이다.
  인스턴스의 정보를 제공한다는 것은 대부분의 경우 인스턴스 변수에 저장된 값들을 문자열로 표현한다는 뜻이다.
  
* 클래스를 작성할 때 toString()을 오버라이딩하지 않는다면, toString()을 호출하면 클래스이름에 16진수의 해시코드를 얻게 될 것이다.

```java
class Card {
    String kind;
    int number;

    Card() {
        this("SPADE", 1);
    }

    Card(String kind, int number) {
        this.kind = kind;
        this.number = number;
    }
}

public class Example {
    public static void main(String[] args) {
        Card c1 = new Card();
        Card c2 = new Card();

        System.out.println(c1.toString());
        System.out.println(c2.toString());
    }
}
```

```
Card@2401f4c3
Card@7637f22
```

* toString()을 오버라이딩하지 않았기 때문에 Object 클래스의 toString()이 호출된다.  
  그래서 클래스이름과 해시코드가 출력되었다.
  
```java
public class Example {
    public static void main(String[] args) {
        String str = new String("KOREA");
        java.util.Date today = new java.util.Date();

        System.out.println(str);
        System.out.println(str.toString());

        System.out.println(today);
        System.out.println(today.toString());
    }
}
```

```
KOREA
KOREA
Mon Apr 05 09:47:45 KST 2021
Mon Apr 05 09:47:45 KST 2021
```

* String 클래스의 toString()은 String 인스턴스가 갖고 있는 문자열을 반환하도록 오버라이딩되어 있고,  
  Date 클래스의 toString()은 Date 인스턴스가 갖고 있는 날짜와 시간을 문자열로 변환하여 반환하도록 오버라이딩되어 있다.
  
* 이처럼 toString()은 일반적으로 인스턴스나 클래스에 대한 정보 또는 인스턴스 변수들의 값을 문자열로 변환하여 반환하도록  
  오버라이딩되는 것이 보통이다.
  
```java
class Card {
    String kind;
    int number;

    Card() {
        this("SPADE", 1);
    }

    Card(String kind, int number) {
        this.kind = kind;
        this.number = number;
    }

    public String toString() {
        return "kind : " + kind + ", number : " + number;
    }
}

public class Example {
    public static void main(String[] args) {
        Card c1 = new Card();
        Card c2 = new Card("HEART", 10);

        System.out.println(c1.toString());
        System.out.println(c2.toString());
    }
}
```

```
kind : SPADE, number : 1
kind : HEART, number : 10
```

## clone()

```java
protected native Object clone() throws CloneNotSupportedException;
```

* 이 메소드는 자신을 복제하여 새로운 인스턴스를 생성하는 일을 한다.

* Object 클래스에 정의된 clone()은 단순히 인스턴스 변수의 값만 복사하기 때문에  
  참조타입의 인스턴스 변수가 있는 클래스는 완전한 복제가 이루어지지 않는다.

* 예를 들어 배열의 경우, 복제된 인스턴스도 같은 배열의 주소를 갖기 때문에 복제된 인스턴스의 작업이 원래의 인스턴스에 영향을 미치게 된다.
  이런 경우 clone 메소드를 오버라이딩해서 새로운 배열을 생성하고 배열의 내용을 복사하도록 해야 한다.

```java
class Point implements Cloneable {
    int x, y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public String toString() {
        return "x=" + x + ", y=" + y;
    }

    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}

public class Example {
    public static void main(String[] args) {
        Point original = new Point(3, 5);
        Point copy = null;

        try {
            copy = (Point)original.clone();
        } catch(CloneNotSupportedException e) {
            e.printStackTrace();
        }

        System.out.println(original);
        System.out.println(copy);
    }
}
```

```
x=3, y=5
x=3, y=5
```

* clone()을 사용하려면, 먼저 복제할 클래스가 Cloneable 인터페이스를 구현해야 하고, clone()을 오버라이딩하면서  
  접근 제어자를 protected에서 public으로 변경한다. 그래야만 상속관계가 없는 다른 클래스에서 clone()을 호출 할 수 있다.

```java
public class Object {
    ...
    protected native Object clone() throws CloneNotSupportedException;
    ...
}
```

* Object 클래스의 clone()은 Cloneable을 구현하지 않은 클래스 내에서 호출되면 CloneNotSupportedException 예외를 발생시킨다.

* 그런데 위 코드와 같이 clone()을 오버라이딩하면 clone()을 호출할 때마다 예외처리를 해야하는 불편함이 있다.

```java
class Point implements Cloneable {
    int x, y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public String toString() {
        return "x=" + x + ", y=" + y;
    }

    public Object clone() {
        Object obj = null;

        try {
            obj = super.clone();
        } catch(CloneNotSupportedException e) {
            e.printStackTrace();
        }

        return obj;
    }
}

public class Example {
    public static void main(String[] args) {
        Point original = new Point(3, 5);
        Point copy = (Point)original.clone();

        System.out.println(original);
        System.out.println(copy);
    }
}
```

* 위와 같이 clone()을 오버라이딩할 때 throws 키워드를 지우고 내부적으로 예외처리하면 호출할 때마다 예외처리를 하지 않아도 된다.

```java
class Point implements Cloneable {  // 1. Cloneable 인터페이스를 구현한다.
    ...
    public Object clone() {         // 2. 접근 제어자를 protected -> public 변경, 3. throws CloneNotSupportedException 삭제.
        Object obj = null;
        
        try {
            obj = super.clone();    // 4. try-catch 내에서 조상 클래스의 clone()을 호출
        } catch(CloneNotSupportedException e) {
            e.printStackTrace();
        }
        
        return obj;
    }
}
```

* Cloneable 인터페이스를 구현한 클래스의 인스턴스만 clone()을 통한 복제가 가능한데, 그 이유는 인스턴스의 데이터를  
  보호하기 위해서이다. Cloneable 인터페이스가 구현되어 있다는 것은 클래스 작성자가 복제를 허용한다는 의미이다.

### 공변 반환타입

* JDK 1.5부터 '공변 반환타입(covariant return type)'이라는 것이 추가되었는데, 이 기능은 오버라이딩할 때  
  조상 메소드의 반환타입을 자손 클래스의 타입으로 변경을 허용하는 것이다.
  
```java
public Point clone() {    // 반환타입을 Object에서 Point로 변경
    Object obj = null;
    
    try {
        obj = super.clone();
    } catch(CloneNotSupportedException e) {
        e.printStackTrace();
    }
    
    return (Point)obj;    // Point 타입으로 형변환하여 반환.
}
```

* 이처럼 '공변 반환타입'을 사용하면, 번거로운 형변환이 줄어든다는 장점이 있다.

```java
Point copy = original.clone();
```

```java
import java.util.Arrays;

public class Example {
    public static void main(String[] args) {
        int[] arr1 = new int[] {1, 2, 3, 4, 5};
        int[] arr2 = arr1.clone();

        arr2[0] = 6;

        System.out.println(Arrays.toString(arr1));
        System.out.println(Arrays.toString(arr2));
    }
}
```

```
[1, 2, 3, 4, 5]
[6, 2, 3, 4, 5]
```

* 배열도 객체이기 때문에 Object 클래스를 상속받으며, 동시에 Cloneable, Serializable 인터페이스가 구현되어 있다.

* clone()을 배열에서는 public으로 오버라이딩하였기 때문에 예제처럼 직접 호출이 가능하다.  
  그리고 원본과 같은 타입을 반환하므로 형변환이 필요 없다.

* 일반적으로는 배열을 복사할 때, 같은 길이의 새로운 배열을 생성한 다음에 `System.arraycopy()`를 이용해서  
  내용을 복사하지만, 이처럼 clone()을 이용해서 간단하게 복사할 수 있다.

```java
int[] arr1 = new int[] {1, 2, 3, 4, 5};
int[] arr2 = arr1.clone();
```

```java
int[] arr1 = new int[] {1, 2, 3, 4, 5};
int[] arr2 = new int[arr1.length];
System.arraycopy(arr1, 0, arr2, 0, arr1.length);
```

```java
public final class System {
    ...
    public static native void arraycopy(Object src, int srcPos, Object dest, int destPos, int length);
    ...
}
```

* 배열 뿐 아니라 java.util 패키지의 Vector, ArrayList, LinkedList, HashSet, TreeSet, HashMap, TreeMap,  
  Calendar, Date와 같은 클래스들이 clone()으로 복제가 가능하다.
  
* clone()으로 복제가 가능한 클래스인지 확인하려면 Java API에서 Cloneable을 구현하였는지 확인하면 된다.

### 얕은 복사와 깊은 복사

* clone()은 단순히 객체에 저장된 값을 그대로 복제할 뿐, 객체가 참조하고 있는 객체까지 복제하지는 않는다.

* 위처럼 기본형 배열인 경우에는 아무런 문제가 없지만, 객체배열을 clone()으로 복제하는 경우에는  
  원본과 복제본이 같은 객체를 공유하므로 완전한 복제라고 보기 어렵다. 

* 이러한 복제를 **'얕은 복사(shallow copy)'** 라고 하며, 얕은 복사에서는 원본을 변경하면 복사본도 영향을 받는다.
  
* 반면에 원본이 참조하고 있는 객체까지 복제하는 것을 **'깊은 복사(deep copy)'** 라고 하며,  
  깊은 복사에서는 원본과 복사본이 서로 다른 객체를 참조하기 때문에 원본의 변경이 복사본에 영향을 미치지 않는다.

```java
class Point {
    int x, y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Circle implements Cloneable {
    Point p;
    double r;

    Circle(Point p, double r) {
        this.p = p;
        this.r = r;
    }

    public Circle shallowCopy() {
        Circle c = null;

        try {
            c = (Circle)super.clone();
        } catch(CloneNotSupportedException e) {}

        return c;
    }

    public Circle deepCopy() {
        Circle c = null;

        try {
            c = (Circle)super.clone();
            c.p = new Point(this.p.x, this.p.y);
        } catch(CloneNotSupportedException e) {}

        return c;
    }
}
```

## getClass()

```java
public final native Class<?> getClass();
```

* 자신이 속한 클래스의 Class 객체를 반환하는 메소드인데, Class 객체는 이름이 'Class'인 클래스의 객체이다.

* Class 객체는 클래스의 모든 정보를 담고 있으며, 클래스 당 1개만 존재한다.  
  클래스 파일이 '클래스 로더(ClassLoader)'에 의해서 메모리에 올라갈 때, 자동으로 생성된다.
  
* 클래스 로더는 실행 시에 필요한 클래스를 동적으로 메모리에 로드하는 역할을 한다.
  * 먼저 기존에 생성된 클래스 객체가 메모리에 존재하는지 확인하고, 있으면 객체의 참조를 반환하고  
    없으면 클래스 패스(classpath)에 지정된 경로를 따라서 클래스 파일을 찾는다.
  
  * 찾지 못하면 ClassNotFoundException이 발생하고, 찾으면 해당 클래스 파일을 읽어서 Class 객체로 반환한다.
  
  * 파일 형태로 저장되어 있는 클래스를 읽어서 Class 클래스에 정의된 형식으로 변환한다.  
    즉, 클래스 파일(.class)을 읽어서 사용하기 편한 형태로 저장해 놓은 것이 클래스 객체이다.

### Class 객체를 얻는 방법

```java
Class c = new Card().getClass();  // 생성된 객체로부터 얻는 방법
Class c = Card.class;             // 클래스 리터럴(*.class)로부터 얻는 방법
Class c = Class.forName("Card");  // 클래스 이름으로부터 얻는 방법
```

* 특히 forName()은 특정 클래스 파일, 예를 들어 데이터베이스 드라이버를 메모리에 올릴 때 주로 사용한다.

* Class 객체를 이용하면 클래스에 정의된 멤버의 이름이나 개수 등, 클래스에 대한 모든 정보를 얻을 수 있기 때문에  
  Class 객체를 통해서 객체를 생성하고 메소드를 호출하는 등 보다 동적인 코드를 작성할 수 있다.
  
```java
Card c = new Card();                // new 연산자를 이용해서 객체 생성
Card c = Card.class.newInstance();  // Class 객체를 이용해서 객체 생성
```

* 동적으로 객체를 생성하고 메소드를 호출하는 방법에 대해 더 알고 싶다면, 'Reflection API'로 검색하면 된다.

```java
final class Card {
    String kind;
    int num;

    Card() {
        this("SPADE", 1);
    }

    Card(String kind, int num) {
        this.kind = kind;
        this.num = num;
    }

    public String toString() {
        return kind + " : " + num;
    }
}

class Example {
    public static void main(String[] args) {
        Card c1 = new Card();
        Card c2 = new Card("HEART", 3);

        Class cObj = c1.getClass();

        System.out.println(c1);
        System.out.println(c2);

        System.out.println(cObj.getName());
        System.out.println(cObj.toGenericString());
        System.out.println(cObj.toString());
    }
}
```

```
SPADE : 1
HEART : 3
Card
final class Card
class Card
```

# 참고

* [자바의 정석](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788994492032&orderClick=LAG&Kc=)
