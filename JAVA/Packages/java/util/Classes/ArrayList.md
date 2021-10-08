# Class ArrayList\<E\>

```java
public class ArrayList<E> extends AbstractList<E> implements List<E>, RandomAccess, Cloneable, java.io.Serializable {
    private static final int DEFAULT_CAPACITY = 10;
    private static final Object[] EMPTY_ELEMENTDATA = {};
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
    
    transient Object[] elementData; // non-private to simplify nested class access
    
    private int size;
    
    public int size() {
        return size;
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
    
    public boolean contains(Object o) {
        return indexOf(o) >= 0;
    }
    
    // (I)List<E> : int indexOf(Object o);
    // (I)List<E> -> (C)AbstractList : public int indexOf(Object o) { ... }
    public int indexOf(Object o) {
        if (o == null) {
            for (int i = 0; i < size; i++)
                if (elementData[i]==null)
                    return i;
        } else {
            for (int i = 0; i < size; i++)
                if (o.equals(elementData[i]))
                    return i;
        }
        return -1;
    }
    
    // (I)List<E> : int lastIndexOf(Object o);
    // (I)List<E> -> (C)AbstractList<E> : public int lastIndexOf(Object o) { ... }
    public int lastIndexOf(Object o) {
        if (o == null) {
            for (int i = size-1; i >= 0; i--)
                if (elementData[i]==null)
                    return i;
        } else {
            for (int i = size-1; i >= 0; i--)
                if (o.equals(elementData[i]))
                    return i;
        }
        return -1;
    }
    
    public Object clone() {
        try {
            ArrayList<?> v = (ArrayList<?>) super.clone();
            v.elementData = Arrays.copyOf(elementData, size);
            v.modCount = 0;
            return v;
        } catch (CloneNotSupportedException e) {
            // this shouldn't happen, since we are Cloneable
            throw new InternalError(e);
        }
    }
    
    public Object[] toArray() {
        return Arrays.copyOf(elementData, size);
    }
    
    @SuppressWarnings("unchecked")
    public <T> T[] toArray(T[] a) {
        if (a.length < size)
            // Make a new array of a's runtime type, but my contents:
            return (T[]) Arrays.copyOf(elementData, size, a.getClass());
        System.arraycopy(elementData, 0, a, 0, size);
        if (a.length > size)
            a[size] = null;
        return a;
    }
    
    // ArrayList<E> Method
    @SuppressWarnings("unchecked")
    E elementData(int index) {
        return (E) elementData[index];
    }
    
    // (I)List<E> : E get(int index);
    // (I)List<E> -> (C)AbstractList<E> : abstract public E get(int index);
    public E get(int index) {
        rangeCheck(index);

        return elementData(index);
    }
    
    public E set(int index, E element) {
        rangeCheck(index);

        E oldValue = elementData(index);
        elementData[index] = element;
        return oldValue;
    }
    
    // (I)Collection<E> : boolean add(E e);
    // (I)Collection<E> -> (C)AbstractCollection<E> : public boolean add(E e) { throw new UnsupportedOperationException(); }
    // (I)Collection<E> -> (C)AbstractCollection<E> -> (C)AbstractList<E> : public boolean add(E e) { ... }
    // (I)Collection<E> -> (I)List<E> : boolean add(E e);
    public boolean add(E e) {
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        elementData[size++] = e;
        return true;
    }
    
    // (I)List<E> : void add(int index, E element)
    // (I)List<E> -> (C)AbstractList<E> : public void add(int index, E element) { throw new UnsupportedOperationException(); }
    public void add(int index, E element) {
        rangeCheckForAdd(index);

        ensureCapacityInternal(size + 1);  // Increments modCount!!
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index);
        elementData[index] = element;
        size++;
    }
    
    public E remove(int index) {
        rangeCheck(index);

        modCount++;
        E oldValue = elementData(index);

        int numMoved = size - index - 1;
        if (numMoved > 0)
            System.arraycopy(elementData, index+1, elementData, index,
                             numMoved);
        elementData[--size] = null; // clear to let GC do its work

        return oldValue;
    }
    
    // (I)Collection<E> : boolean remove(Object o);
    // (I)Collection<E> -> (C)AbstractCollection<E> : public boolean remove(Object o) { ... }
    public boolean remove(Object o) {
        if (o == null) {
            for (int index = 0; index < size; index++)
                if (elementData[index] == null) {
                    fastRemove(index);
                    return true;
                }
        } else {
            for (int index = 0; index < size; index++)
                if (o.equals(elementData[index])) {
                    fastRemove(index);
                    return true;
                }
        }
        return false;
    }
    
    public void clear() {
        modCount++;

        // clear to let GC do its work
        for (int i = 0; i < size; i++)
            elementData[i] = null;

        size = 0;
    }
    
    // (I)Collection<E> : boolean addAll(Collection<? extends E> c);
    // (I)Collection<E> -> (C)AbstractCollection<E> : public boolean addAll(Collection<? extends E> c) { ... }
    public boolean addAll(Collection<? extends E> c) {
        Object[] a = c.toArray();
        int numNew = a.length;
        ensureCapacityInternal(size + numNew);  // Increments modCount
        System.arraycopy(a, 0, elementData, size, numNew);
        size += numNew;
        return numNew != 0;
    }
    
    // (I)List<E> : boolean addAll(int index Collection<? extends E> c);
    // (I)List<E> -> (C)AbstractList<E> : public boolean addAll(int index Collection<? extends E> c) { ... }
    public boolean addAll(int index, Collection<? extends E> c) {
        rangeCheckForAdd(index);

        Object[] a = c.toArray();
        int numNew = a.length;
        ensureCapacityInternal(size + numNew);  // Increments modCount

        int numMoved = size - index;
        if (numMoved > 0)
            System.arraycopy(elementData, index, elementData, index + numNew,
                             numMoved);

        System.arraycopy(a, 0, elementData, index, numNew);
        size += numNew;
        return numNew != 0;
    }
    
    ...
}
```
