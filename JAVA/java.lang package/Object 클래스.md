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
  
* `System.identityHashCode(Object x)`는 Object 클래스의 hashCode 메소드처럼 객체의 주소값으로 해시코드를 생성하기 때문에  
  모든 객체에 대해 항상 다른 해시코드값을 반환할 것을 보장한다. 그래서 str1와 str2가 해시코드는 같지만 서로 다른 객체라는 것을 알 수 있다.
  
* `System.identityHashCode(Object x)`의 호출결과는 실행 할 때마다 달라질 수 있다.

## toString()

## clone()

## getClass()
