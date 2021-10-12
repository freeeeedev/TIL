# Class Arrays

```java
public static void sort(byte[] a) {
    DualPivotQuicksort.sort(a, 0, a.length - 1);
}

public static void sort(short[] a) {
    DualPivotQuicksort.sort(a, 0, a.length - 1, null, 0, 0);
}

public static void sort(int[] a) {
    DualPivotQuicksort.sort(a, 0, a.length - 1, null, 0, 0);
}

public static void sort(long[] a) {
    DualPivotQuicksort.sort(a, 0, a.length - 1, null, 0, 0);
}

public static void sort(char[] a) {
    DualPivotQuicksort.sort(a, 0, a.length - 1, null, 0, 0);
}

public static void sort(float[] a) {
    DualPivotQuicksort.sort(a, 0, a.length - 1, null, 0, 0);
}

public static void sort(double[] a) {
    DualPivotQuicksort.sort(a, 0, a.length - 1, null, 0, 0);
}

public static void sort(Object[] a) {
    if (LegacyMergeSort.userRequested)
        legacyMergeSort(a);
    else
        ComparableTimSort.sort(a, 0, a.length, null, 0, 0);
}

public static <T> void sort(T[] a, Comparator<? super T> c) {
    if (c == null) {
        sort(a);
    } else {
        if (LegacyMergeSort.userRequested)
            legacyMergeSort(a, c);
        else
            TimSort.sort(a, 0, a.length, c, null, 0, 0);
    }
}
```

```java
public static void sort(byte[] a, int fromIndex, int toIndex) {
    rangeCheck(a.length, fromIndex, toIndex);
    DualPivotQuicksort.sort(a, fromIndex, toIndex - 1);
}

public static void sort(short[] a, int fromIndex, int toIndex) {
    rangeCheck(a.length, fromIndex, toIndex);
    DualPivotQuicksort.sort(a, fromIndex, toIndex - 1, null, 0, 0);
}

public static void sort(int[] a, int fromIndex, int toIndex) {
    rangeCheck(a.length, fromIndex, toIndex);
    DualPivotQuicksort.sort(a, fromIndex, toIndex - 1, null, 0, 0);
}

public static void sort(long[] a, int fromIndex, int toIndex) {
    rangeCheck(a.length, fromIndex, toIndex);
    DualPivotQuicksort.sort(a, fromIndex, toIndex - 1, null, 0, 0);
}

public static void sort(char[] a, int fromIndex, int toIndex) {
    rangeCheck(a.length, fromIndex, toIndex);
    DualPivotQuicksort.sort(a, fromIndex, toIndex - 1, null, 0, 0);
}

public static void sort(float[] a, int fromIndex, int toIndex) {
    rangeCheck(a.length, fromIndex, toIndex);
    DualPivotQuicksort.sort(a, fromIndex, toIndex - 1, null, 0, 0);
}

public static void sort(double[] a, int fromIndex, int toIndex) {
    rangeCheck(a.length, fromIndex, toIndex);
    DualPivotQuicksort.sort(a, fromIndex, toIndex - 1, null, 0, 0);
}

public static void sort(Object[] a, int fromIndex, int toIndex) {
    rangeCheck(a.length, fromIndex, toIndex);
    if (LegacyMergeSort.userRequested)
        legacyMergeSort(a, fromIndex, toIndex);
    else
        ComparableTimSort.sort(a, fromIndex, toIndex, null, 0, 0);
}

public static <T> void sort(T[] a, int fromIndex, int toIndex, Comparator<? super T> c) {
    if (c == null) {
        sort(a, fromIndex, toIndex);
    } else {
        rangeCheck(a.length, fromIndex, toIndex);
        if (LegacyMergeSort.userRequested)
            legacyMergeSort(a, fromIndex, toIndex, c);
        else
            TimSort.sort(a, fromIndex, toIndex, c, null, 0, 0);
    }
}
```

```java
public static int binarySearch(byte[] a, byte key) {
    return binarySearch0(a, 0, a.length, key);
}

public static int binarySearch(short[] a, short key) {
    return binarySearch0(a, 0, a.length, key);
}

public static int binarySearch(int[] a, int key) {
    return binarySearch0(a, 0, a.length, key);
}

public static int binarySearch(long[] a, long key) {
    return binarySearch0(a, 0, a.length, key);
}

public static int binarySearch(char[] a, char key) {
    return binarySearch0(a, 0, a.length, key);
}

public static int binarySearch(float[] a, float key) {
    return binarySearch0(a, 0, a.length, key);
}

public static int binarySearch(double[] a, double key) {
    return binarySearch0(a, 0, a.length, key);
}

public static int binarySearch(Object[] a, Object key) {
    return binarySearch0(a, 0, a.length, key);
}

public static <T> int binarySearch(T[] a, T key, Comparator<? super T> c) {
    return binarySearch0(a, 0, a.length, key, c);
}
```

```java
public static int binarySearch(byte[] a, int fromIndex, int toIndex, byte key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

public static int binarySearch(short[] a, int fromIndex, int toIndex, short key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

public static int binarySearch(int[] a, int fromIndex, int toIndex, int key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

public static int binarySearch(long[] a, int fromIndex, int toIndex, long key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

public static int binarySearch(char[] a, int fromIndex, int toIndex, char key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

public static int binarySearch(float[] a, int fromIndex, int toIndex, float key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

public static int binarySearch(double[] a, int fromIndex, int toIndex, double key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

public static int binarySearch(Object[] a, int fromIndex, int toIndex, Object key) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key);
}

public static <T> int binarySearch(T[] a, int fromIndex, int toIndex, T key, Comparator<? super T> c) {
    rangeCheck(a.length, fromIndex, toIndex);
    return binarySearch0(a, fromIndex, toIndex, key, c);
}
```

```java
private static int binarySearch0(byte[] a, int fromIndex, int toIndex, byte key) { ... }

private static int binarySearch0(short[] a, int fromIndex, int toIndex, short key) { ... }

private static int binarySearch0(int[] a, int fromIndex, int toIndex, int key) {
    int low = fromIndex;
    int high = toIndex - 1;

    while (low <= high) {
        int mid = (low + high) >>> 1;
        int midVal = a[mid];

        if (midVal < key)
            low = mid + 1;
        else if (midVal > key)
            high = mid - 1;
        else
            return mid; // key found
    }
    return -(low + 1);  // key not found.
}

private static int binarySearch0(long[] a, int fromIndex, int toIndex, long key) { ... }

private static int binarySearch0(char[] a, int fromIndex, int toIndex, char key) { ... }

private static int binarySearch0(float[] a, int fromIndex, int toIndex, float key) {
    int low = fromIndex;
    int high = toIndex - 1;

    while (low <= high) {
        int mid = (low + high) >>> 1;
        float midVal = a[mid];

        if (midVal < key)
            low = mid + 1;  // Neither val is NaN, thisVal is smaller
        else if (midVal > key)
            high = mid - 1; // Neither val is NaN, thisVal is larger
        else {
            int midBits = Float.floatToIntBits(midVal);
            int keyBits = Float.floatToIntBits(key);
            if (midBits == keyBits)     // Values are equal
                return mid;             // Key found
            else if (midBits < keyBits) // (-0.0, 0.0) or (!NaN, NaN)
                low = mid + 1;
            else                        // (0.0, -0.0) or (NaN, !NaN)
                high = mid - 1;
        }
    }
    return -(low + 1);  // key not found.
}

private static int binarySearch0(double[] a, int fromIndex, int toIndex, double key) {
    int low = fromIndex;
    int high = toIndex - 1;

    while (low <= high) {
        int mid = (low + high) >>> 1;
        double midVal = a[mid];

        if (midVal < key)
            low = mid + 1;  // Neither val is NaN, thisVal is smaller
        else if (midVal > key)
            high = mid - 1; // Neither val is NaN, thisVal is larger
        else {
            long midBits = Double.doubleToLongBits(midVal);
            long keyBits = Double.doubleToLongBits(key);
            if (midBits == keyBits)     // Values are equal
                return mid;             // Key found
            else if (midBits < keyBits) // (-0.0, 0.0) or (!NaN, NaN)
                low = mid + 1;
            else                        // (0.0, -0.0) or (NaN, !NaN)
                high = mid - 1;
        }
    }
    return -(low + 1);  // key not found.
}

private static int binarySearch0(Object[] a, int fromIndex, int toIndex, Object key) {
    int low = fromIndex;
    int high = toIndex - 1;

    while (low <= high) {
        int mid = (low + high) >>> 1;
        @SuppressWarnings("rawtypes")
        Comparable midVal = (Comparable)a[mid];
        @SuppressWarnings("unchecked")
        int cmp = midVal.compareTo(key);

        if (cmp < 0)
            low = mid + 1;
        else if (cmp > 0)
            high = mid - 1;
        else
            return mid; // key found
    }
    return -(low + 1);  // key not found.
}

private static <T> int binarySearch0(T[] a, int fromIndex, int toIndex, T key, Comparator<? super T> c) {
    if (c == null) {
        return binarySearch0(a, fromIndex, toIndex, key);
    }
    int low = fromIndex;
    int high = toIndex - 1;

    while (low <= high) {
        int mid = (low + high) >>> 1;
        T midVal = a[mid];
        int cmp = c.compare(midVal, key);
        if (cmp < 0)
            low = mid + 1;
        else if (cmp > 0)
            high = mid - 1;
        else
            return mid; // key found
    }
    return -(low + 1);  // key not found.
}
```

```java
public class Arrays {
    ...
    private static class ArrayList<E> extends AbstractList<E> implements RandomAccess, java.io.Serializable {
        private static final long serialVersionUID = -2764017481108945198L;
        private final E[] a;

        ArrayList(E[] array) {
            a = Objects.requireNonNull(array);
        }

        @Override
        public int size() {
            return a.length;
        }

        @Override
        public Object[] toArray() {
            return a.clone();
        }

        @Override
        @SuppressWarnings("unchecked")
        public <T> T[] toArray(T[] a) {
            int size = size();
            if (a.length < size)
                return Arrays.copyOf(this.a, size,
                                     (Class<? extends T[]>) a.getClass());
            System.arraycopy(this.a, 0, a, 0, size);
            if (a.length > size)
                a[size] = null;
            return a;
        }

        @Override
        public E get(int index) {
            return a[index];
        }

        @Override
        public E set(int index, E element) {
            E oldValue = a[index];
            a[index] = element;
            return oldValue;
        }

        @Override
        public int indexOf(Object o) {
            E[] a = this.a;
            if (o == null) {
                for (int i = 0; i < a.length; i++)
                    if (a[i] == null)
                        return i;
            } else {
                for (int i = 0; i < a.length; i++)
                    if (o.equals(a[i]))
                        return i;
            }
            return -1;
        }

        @Override
        public boolean contains(Object o) {
            return indexOf(o) != -1;
        }

        @Override
        public Spliterator<E> spliterator() {
            return Spliterators.spliterator(a, Spliterator.ORDERED);
        }

        @Override
        public void forEach(Consumer<? super E> action) {
            Objects.requireNonNull(action);
            for (E e : a) {
                action.accept(e);
            }
        }

        @Override
        public void replaceAll(UnaryOperator<E> operator) {
            Objects.requireNonNull(operator);
            E[] a = this.a;
            for (int i = 0; i < a.length; i++) {
                a[i] = operator.apply(a[i]);
            }
        }

        @Override
        public void sort(Comparator<? super E> c) {
            Arrays.sort(a, c);
        }
    }
    
    @SafeVarargs
    @SuppressWarnings("varargs")
    public static <T> List<T> asList(T... a) {
        return new ArrayList<>(a);
    }
    
    ...
}
```

```java

```
