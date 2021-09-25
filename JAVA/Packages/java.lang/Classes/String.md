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

### String toLowerCase()

* default locale 규칙을 사용하여 String 인스턴스에 저장되어 있는 모든 문자를 소문자로 변환하여 반환한다.

```java
public String toLowerCase() {
    return toLowerCase(Locale.getDefault());
}
```

### String toLowerCase(Locale locale)

* 주어진 locale 규칙을 사용하여 String 인스턴스에 저장되어 있는 모든 문자를 소문자로 변환하여 반환한다.

### String toUpperCase()

* default locale 규칙을 사용하여 String 인스턴스에 저장되어 있는 모든 문자를 대문자로 변환하여 반환한다.

```java
public String toUpperCase() {
    return toUpperCase(Locale.getDefault());
}
```

### String toUpperCase(Locale locale)

* 주어진 locale 규칙을 사용하여 String 인스턴스에 저장되어 있는 모든 문자를 대문자로 변환하여 반환한다.

### boolean startsWith(String prefix)

* 주어진 문자열(prefix)로 시작하는지 검사한다.

```java
public boolean startsWith(String prefix) {
    return startsWith(prefix, 0);
}
```

### boolean startsWith(String prefix, int toffset)

* 주어진 위치(toffset)부터 주어진 문자열(prefix)로 시작하는지 검사한다.

```java
public boolean startsWith(String prefix, int toffset) {
    char ta[] = value;
    int to = toffset;
    char pa[] = prefix.value;
    int po = 0;
    int pc = prefix.value.length;
    // Note: toffset might be near -1>>>1.
    if ((toffset < 0) || (toffset > value.length - pc)) {
        return false;
    }
    while (--pc >= 0) {
        if (ta[to++] != pa[po++]) {
            return false;
        }
    }
    return true;
}
```

### boolean endsWith(String suffix)

* 주어진 문자열(suffix)로 끝나는지 검사한다.

```java
public boolean endsWith(String suffix) {
    return startsWith(suffix, value.length - suffix.value.length);
}
```

### int hashCode()

* String 인스턴스에 저장되어있는 문자열의 해시코드를 반환한다.
* 해시코드를 한 번 구한 이후에는(hash != 0) hash값을 그대로 반환한다.

```java
public int hashCode() {
    int h = hash;
    if (h == 0 && value.length > 0) {
        char val[] = value;

        for (int i = 0; i < value.length; i++) {
            h = 31 * h + val[i];
        }
        hash = h;
    }
    return h;
}
```

### String[] split(String regex)

* 문자열을 지정된 분리자(regex)로 나누어 문자열 배열에 담아 반환한다.

```java
public String[] split(String regex) {
    return split(regex, 0);
}
```

### String[] split(String regex, int limit)

* 문자열을 지정된 분리자(regex)로 나누어 문자열 배열에 담아 반환한다.
* 단, 문자열 전체를 지정된 수(limit)로 자른다.

### static String join(CharSequence delimiter, CharSequence... elements)

* 주어진 문자열들(elements) 사이에 구분자(delimiter)를 넣어서 결합한다.

```java
public static String join(CharSequence delimiter, CharSequence... elements) {
    Objects.requireNonNull(delimiter);
    Objects.requireNonNull(elements);
    // Number of elements not likely worth Arrays.stream overhead.
    StringJoiner joiner = new StringJoiner(delimiter);
    for (CharSequence cs: elements) {
        joiner.add(cs);
    }
    return joiner.toString();
}
```

```java
class Example {
    public static void main(String[] args) {
        String animals = "dog,cat,bear";
        String[] arr = animals.split(",");

        String str = String.join("-", arr);
        System.out.println(str);
    }
}
```

```
dog-cat-bear
```

### static String join(CharSequence delimiter, Iterable\<? extends CharSequence\> elements)

* Iterable\<? extends CharSequence\> 인터페이스를 구현한 클래스의 인스턴스에 담겨있는 문자열들 사이에 구분자를 넣어서 결합한다.

```java
public static String join(CharSequence delimiter, Iterable<? extends CharSequence> elements) {
    Objects.requireNonNull(delimiter);
    Objects.requireNonNull(elements);
    StringJoiner joiner = new StringJoiner(delimiter);
    for (CharSequence cs: elements) {
        joiner.add(cs);
    }
    return joiner.toString();
}
```

### char[] toCharArray()

* String 인스턴스의 문자열을 char 배열로 변환하여 반환한다.

```java
public char[] toCharArray() {
    // Cannot use Arrays.copyOf because of class initialization order issues
    char result[] = new char[value.length];
    System.arraycopy(value, 0, result, 0, value.length);
    return result;
}
```

### String replace(char oldChar, char newChar)

* 문자열 중의 문자(oldChar)를 새로운 문자(newChar)로 모두 바꾼 문자열을 반환한다.

```java
public String replace(char oldChar, char newChar) {
    if (oldChar != newChar) {
        int len = value.length;
        int i = -1;
        char[] val = value; /* avoid getfield opcode */

        while (++i < len) {
            if (val[i] == oldChar) {
                break;
            }
        }
        if (i < len) {
            char buf[] = new char[len];
            for (int j = 0; j < i; j++) {
                buf[j] = val[j];
            }
            while (i < len) {
                char c = val[i];
                buf[i] = (c == oldChar) ? newChar : c;
                i++;
            }
            return new String(buf, true);
        }
    }
    return this;
}
```

### String replace(CharSequence target, CharSequence replacement)

* 문자열 중에서 문자열(target)을 새로운 문자열(replacement)로 모두 바꾼 문자열을 반환한다

### String replaceFirst(String regex, String replacement)

* 문자열 중에서 문자열(regex)과 일치하는 것 중, 첫 번째 것만 새로운 문자열(replacement)로 바꾼 문자열을 반환한다.

### String replaceAll(String regex, String replacement)

* 문자열 중에서 문자열(regex)과 일치하는 것을 새로운 문자열(replacement)로 모두 바꾼 문자열을 반환한다.

### boolean contains(CharSequence s)

* 문자열에 지정된 문자열(s)이 포함되었는지 검사한다.

```java
public boolean contains(CharSequence s) {
    return indexOf(s.toString()) > -1;
}
```

### int indexOf(int ch)

* 주어진 문자(ch)가 문자열에 존재하는지 확인하여 위치(index)를 반환한다.
* 못 찾으면 -1을 반환한다.

```java
public int indexOf(int ch) {
    return indexOf(ch, 0);
}
```

### int indexOf(int ch, int fromIndex)

* 주어진 문자(ch)가 문자열에 존재하는지 지정된 위치(fromIndex)부터 확인하여 위치(index)를 반환한다.
* 못 찾으면 -1을 반환한다.

```java
public int indexOf(int ch, int fromIndex) {
    final int max = value.length;
    if (fromIndex < 0) {
        fromIndex = 0;
    } else if (fromIndex >= max) {
        // Note: fromIndex might be near -1>>>1.
        return -1;
    }

    if (ch < Character.MIN_SUPPLEMENTARY_CODE_POINT) {
        // handle most cases here (ch is a BMP code point or a
        // negative value (invalid code point))
        final char[] value = this.value;
        for (int i = fromIndex; i < max; i++) {
            if (value[i] == ch) {
                return i;
            }
        }
        return -1;
    } else {
        return indexOfSupplementary(ch, fromIndex);
    }
}
```

### int indexOf(String str)

* 주어진 문자열(str)이 문자열에 존재하는지 확인하여 위치(index)를 반환한다.
* 못 찾으면 -1을 반환한다.

```java
public int indexOf(String str) {
    return indexOf(str, 0);
}
```

### int indexOf(String str, int fromIndex)

* 주어진 문자열(str)이 문자열에 존재하는지 지정된 위치(fromIndex)부터 확인하여 위치(index)를 반환한다.
* 못 찾으면 -1을 반환한다.

```java
public int indexOf(String str, int fromIndex) {
    return indexOf(value, 0, value.length, str.value, 0, str.value.length, fromIndex);
}
```

### static int indexOf(char[] source, int sourceOffset, int sourceCount,
###                   char[] target, int targetOffset, int targetCount,
###                     int fromIndex)

```java
static int indexOf(char[] source, int sourceOffset, int sourceCount,
                   char[] target, int targetOffset, int targetCount,
                   int fromIndex) {
    if (fromIndex >= sourceCount) {
        return (targetCount == 0 ? sourceCount : -1);
    }
    if (fromIndex < 0) {
        fromIndex = 0;
    }
    if (targetCount == 0) {
        return fromIndex;
    }

    char first = target[targetOffset];
    int max = sourceOffset + (sourceCount - targetCount);

    for (int i = sourceOffset + fromIndex; i <= max; i++) {
        /* Look for first character. */
        if (source[i] != first) {
            while (++i <= max && source[i] != first);
        }

        /* Found first character, now look at the rest of v2 */
        if (i <= max) {
            int j = i + 1;
            int end = j + targetCount - 1;
            for (int k = targetOffset + 1; j < end && source[j] == target[k]; j++, k++);

            if (j == end) {
                /* Found whole string. */
                return i - sourceOffset;
            }
        }
    }
    return -1;
}
```

### int lastIndexOf(int ch)

* 주어진 문자(ch)를 문자열의 오른쪽 끝에서부터 왼쪽으로 존재하는지 확인하여 위치(index)를 반환한다.
* 못 찾으면 -1을 반환한다.

```java
public int lastIndexOf(int ch) {
    return lastIndexOf(ch, value.length - 1);
}
```

### int lastIndexOf(int ch, int fromIndex)

* 주어진 문자(ch)를 문자열의 지정된 위치(fromIndex)부터 왼쪽으로 존재하는지 확인하여 위치(index)를 반환한다.
* 못 찾으면 -1을 반환한다.

```java
public int lastIndexOf(int ch, int fromIndex) {
    if (ch < Character.MIN_SUPPLEMENTARY_CODE_POINT) {
        // handle most cases here (ch is a BMP code point or a
        // negative value (invalid code point))
        final char[] value = this.value;
        int i = Math.min(fromIndex, value.length - 1);
        for (; i >= 0; i--) {
            if (value[i] == ch) {
                return i;
            }
        }
        return -1;
    } else {
        return lastIndexOfSupplementary(ch, fromIndex);
    }
}
```

### int lastIndexOf(String str)

* 주어진 문자열(str)를 문자열의 오른쪽 끝에서부터 왼쪽으로 존재하는지 확인하여 위치(index)를 반환한다.
* 못 찾으면 -1을 반환한다.

```java
public int lastIndexOf(String str) {
    return lastIndexOf(str, value.length);
}
```

### int lastIndexOf(String str, int fromIndex)

* 주어진 문자열(str)를 문자열의 지정된 위치(fromIndex)부터 왼쪽으로 존재하는지 확인하여 위치(index)를 반환한다.
* 못 찾으면 -1을 반환한다.

```java
public int lastIndexOf(String str, int fromIndex) {
    return lastIndexOf(value, 0, value.length, str.value, 0, str.value.length, fromIndex);
}
```

### static String valueOf()

* 주어진 값을 문자열로 변환하여 반환한다.

```java
public static String valueOf(boolean b) {
    return b ? "true" : "false";
}

public static String valueOf(char c) {
    char data[] = {c};
    return new String(data, true);
}    

public static String valueOf(int i) {
    return Integer.toString(i);
}

public static String valueOf(long l) {
    return Long.toString(l);
}

public static String valueOf(float f) {
    return Float.toString(f);
}

public static String valueOf(double d) {
    return Double.toString(d);
}

public static String valueOf(Object obj) {
    return (obj == null) ? "null" : obj.toString();
}

public static String valueOf(char data[]) {
    return new String(data);
}

public static String valueOf(char data[], int offset, int count) {
    return new String(data, offset, count);
}
```
