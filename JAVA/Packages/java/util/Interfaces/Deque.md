# Interface Deque\<E\>

```java
public interface Deque<E> extends Queue<E> {
    void addFirst(E e);
    
    void addLast(E e);
    
    boolean offerFirst(E e);
    
    boolean offerLast(E e);
    
    E removeFirst();
    
    E removeLast();
    
    E pollFirst();
    
    E pollLast();
    
    E getFirst();
    
    E getLast();
    
    E peekFirst();
    
    E peekLast();
    
    boolean removeFirstOccurrence(Object o);
    
    boolean removeLastOccurrence(Object o);
    
    // *** Queue methods ***
    
    boolean add(E e);
    
    boolean offer(E e);
    
    E remove();
    
    E poll();
    
    E element();
    
    E peek();
    
    // *** Stack methods ***
    
    void push(E e);
    
    E pop();
    
    // *** Collection methods ***
    
    boolean remove(Object o);
    
    boolean contains(Object o);
    
    public int size();
    
    Iterator<E> iterator();
    
    Iterator<E> descendingIterator();
}
```
