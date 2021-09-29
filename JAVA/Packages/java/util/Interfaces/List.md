# Interface List\<E\>

```java
public interface List<E> extends Collection<E> {
    int size();
    
    boolean isEmpty();
    
    boolean contains(Object o);
    
    Iterator<E> iterator();
    
    Object[] toArray();
    
    <T> T[] toArray(T[] a);
    
    boolean add(E e);
    
    boolean remove(Object o);
    
    boolean containsAll(Collection<?> c);
    
    boolean addAll(Collection<? extends E> c);
    
    // List
    boolean addAll(int index, Collection<? extends E> c);
    
    boolean removeAll(Collection<?> c);
    
    boolean retainAll(Collection<?> c);
    
    // List
    default void replaceAll(UnaryOperator<E> operator) {
        Objects.requireNonNull(operator);
        final ListIterator<E> li = this.listIterator();
        while (li.hasNext()) {
            li.set(operator.apply(li.next()));
        }
    }
    
    // List
    @SuppressWarnings({"unchecked", "rawtypes"})
    default void sort(Comparator<? super E> c) {
        Object[] a = this.toArray();
        Arrays.sort(a, (Comparator) c);
        ListIterator<E> i = this.listIterator();
        for (Object e : a) {
            i.next();
            i.set((E) e);
        }
    }
    
    void clear();
    
    boolean equals(Object o);
    
    int hashCode();
    
    // ------------------------- List -------------------------
    
    E get(int index);
    
    E set(int index, E element);
    
    void add(int index, E element);
    
    E remove(int index);
    
    int indexOf(Object o);
    
    int lastIndexOf(Object o);
    
    ListIterator<E> listIterator();
    
    ListIterator<E> listIterator(int index);
    
    List<E> subList(int fromIndex, int toIndex);
    
    @Override
    default Spliterator<E> spliterator() {
        return Spliterators.spliterator(this, Spliterator.ORDERED);
    }
}
```
