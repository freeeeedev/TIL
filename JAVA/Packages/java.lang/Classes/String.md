# Class String

```java
public final class String implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];

    /** Cache the hash code for the string. */
    private int hash; // Default to 0
    ...
}
```

## Fields

## Constructors

### String()

* 빈 문자열("")을 갖는 String 인스턴스를 생성한다.

```java
public String() {
    this.value = "".value;
}
```

### String(String original)

* 주어진 문자열을 갖는 String 인스턴스를 생성한다.

```java
public String(String original) {
    this.value = original.value;
    this.hash = original.hash;
}
```

### String(char[] value)

* char 배열에 해당하는 문자열을 갖는 String 인스턴스를 생성한다.

```java
public String(char value[]) {
    this.value = Arrays.copyOf(value, value.length);
}
```

### String(char[] value, int offset, int count)

* char 배열의 offset 위치부터 count개 만큼의 문자열을 갖는 String 인스턴스를 생성한다.

```java
public String(char value[], int offset, int count) {
    if (offset < 0) {
        throw new StringIndexOutOfBoundsException(offset);
    }
    if (count <= 0) {
        if (count < 0) {
            throw new StringIndexOutOfBoundsException(count);
        }
        if (offset <= value.length) {
            this.value = "".value;
            return;
        }
    }
    // Note: offset or count might be near -1>>>1.
    if (offset > value.length - count) {
        throw new StringIndexOutOfBoundsException(offset + count);
    }
    this.value = Arrays.copyOfRange(value, offset, offset+count);
}
```

### String(StringBuffer buffer)

* StringBuffer 인스턴스가 갖고 있는 문자열과 같은 내용의 String 인스턴스를 생성한다.

```java
public String(StringBuffer buffer) {
    synchronized(buffer) {
        this.value = Arrays.copyOf(buffer.getValue(), buffer.length());
    }
}
```

### String(StringBuilder builder)

* StringBuilder 인스턴스가 갖고 있는 문자열과 같은 내용의 String 인스턴스를 생성한다.

```java
public String(StringBuilder builder) {
    this.value = Arrays.copyOf(builder.getValue(), builder.length());
}
```

## All Methods

### String toString()

* String 인스턴스에 저장되어 있는 문자열을 반환한다.

```java
public String toString() {
    return this;
}
```

### char charAt(int index)

* 지정된 위치(index)에 있는 문자를 알려준다. (index는 0부터 시작)

```java
public char charAt(int index) {
    if ((index < 0) || (index >= value.length)) {
        throw new StringIndexOutOfBoundsException(index);
    }
    return value[index];
}
```

### int length()

* 문자열의 길이를 알려준다.

```java
public int length() {
    return value.length;
}
```

### boolean isEmpty()

* 빈 문자열인지 알려준다.

```java
public boolean isEmpty() {
    return value.length == 0;
}
```

### boolean equals(Object anObject)

* String 인스턴스의 문자열과 매개변수로 받은 문자열(anObject)을 비교한다.
* anObject가 String이 아니거나 문자열이 다르면 false를 반환한다.

```java
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            while (n-- != 0) {
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}
```

### boolean equalsIgnoreCase(String anotherString)

* String 인스턴스의 문자열과 매개변수로 받은 문자열(anotherString)을 대소문자 구분없이 비교한다.

```java
public boolean equalsIgnoreCase(String anotherString) {
    return (this == anotherString) ? true
            : (anotherString != null)
            && (anotherString.value.length == value.length)
            && regionMatches(true, 0, anotherString, 0, value.length);
}
```

* 문자열에 영문자가 아닌 다른 문자가 섞여있어도 정상적으로 동작한다.

```java
class Example {
    public static void main(String[] args) {
        String str1 = "ABC123!@#abc";
        String str2 = "abc123!@#ABC";

        System.out.println(str1.equalsIgnoreCase(str2));
    }
}
```

```
true
```

### int compareTo(String anotherString)

* 문자열(anotherString)과 사전 순서로 비교한다.
* 사전 순으로 같으면 0, 이전이면 음수, 이후면 양수를 반환한다.

```java
public int compareTo(String anotherString) {
    int len1 = value.length;
    int len2 = anotherString.value.length;
    int lim = Math.min(len1, len2);
    char v1[] = value;
    char v2[] = anotherString.value;

    int k = 0;
    while (k < lim) {
        char c1 = v1[k];
        char c2 = v2[k];
        if (c1 != c2) {
            return c1 - c2;
        }
        k++;
    }
    return len1 - len2;
}
```

### String substring(int beginIndex)

* 주어진 위치(beginIndex)부터 시작하는 문자열을 얻는다.

```java
public String substring(int beginIndex) {
    if (beginIndex < 0) {
        throw new StringIndexOutOfBoundsException(beginIndex);
    }
    int subLen = value.length - beginIndex;
    if (subLen < 0) {
        throw new StringIndexOutOfBoundsException(subLen);
    }
    return (beginIndex == 0) ? this : new String(value, beginIndex, subLen);
}
```

### String substring(int beginIndex, int endIndex)

* 주어진 시작 위치(beginIndex)부터 끝 위치(endIndex) 범위에 포함된 문자열을 얻는다.
* 이 때, 시작 위치의 문자는 범위에 포함되지만, 끝 위치의 문자는 범위에 포함되지 않는다. (beginIndex <= x < endIndex)

```java
public String substring(int beginIndex, int endIndex) {
    if (beginIndex < 0) {
        throw new StringIndexOutOfBoundsException(beginIndex);
    }
    if (endIndex > value.length) {
        throw new StringIndexOutOfBoundsException(endIndex);
    }
    int subLen = endIndex - beginIndex;
    if (subLen < 0) {
        throw new StringIndexOutOfBoundsException(subLen);
    }
    return ((beginIndex == 0) && (endIndex == value.length)) ? this
            : new String(value, beginIndex, subLen);
}
```

### String trim()

* 문자열의 왼쪽 끝과 오른쪽 끝에 있는 공백을 없앤 결과를 반환한다.
* 이 때 문자열 중간에 있는 공백은 제거되지 않는다.
* 공백 ' ' 뿐만 아니라 아스키코드 ' ' 이하의 모든 공백이 제거된다.

```java
public String trim() {
    int len = value.length;
    int st = 0;
    char[] val = value;    /* avoid getfield opcode */

    while ((st < len) && (val[st] <= ' ')) {
        st++;
    }
    while ((st < len) && (val[len - 1] <= ' ')) {
        len--;
    }
    return ((st > 0) || (len < value.length)) ? substring(st, len) : this;
}
```
