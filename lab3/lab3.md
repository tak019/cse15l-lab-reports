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
