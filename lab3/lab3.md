#Lab Report 3

Failure-inducing input:
```
public class LinkedListTest {

    @Test(expected = NoSuchElementException.class)
    public void testLastEmptyList() {
        LinkedList list = new LinkedList();
        list.last();
    }
}
```
---
Non-failure-inducing input:
```
public class LinkedListTest {

    @Test
    public void testLastNonEmptyList() {
        LinkedList list = new LinkedList();
        list.append(1);
        assertEquals(1, list.last());
    }
}
```
