# Interface Map.Entry\<K, V\>

```java
interface Entry<K,V> {
    K getKey();
    
    V getValue();
    
    V setValue(V value);
    
    boolean equals(Object o);
    
    int hashCode();
    
    ...
}
```
