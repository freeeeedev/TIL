# Interface ListIterator\<E\>

```java
public interface ListIterator<E> extends Iterator<E> {
    // Iterator
    boolean hasNext();
    
    // Iterator
    E next();
    
    boolean hasPrevious();
    
    E previous();
    
    int nextIndex();
    
    int previousIndex();
    
    // Iterator
    void remove();
    
    void set(E e);
    
    void add(E e);
}
```
