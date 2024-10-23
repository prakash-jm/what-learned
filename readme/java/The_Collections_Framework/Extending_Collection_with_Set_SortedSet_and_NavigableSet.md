[The Collection FrameWork](./README.md) |  [Extending Collection with List](./Extending_Collection_with_List.md)| Extending Collection with Set, SortedSet and NavigableSet | [Creating and Processing Data with the Collections Factory Methods](./Creating_and_Processing_Data_with_the_Collections_Factory_Methods.md)
##### Exploring the Set Interface
* The Set interface does not bring any new method to the Collection interface. The Collections Framework gives you one plain implementation of the Set interface: HashSet. Internally, a HashSet wraps an instance of HashMap, a class that will be covered later, that acts as a delegate for HashSet. 
* As you already saw, what a Set brings to a Collection is that it forbids duplicates. What you lose over the List interface is that your elements are stored in no particular order. There is very little chance that you will iterate over them in the same order as you added them to your set. 
* You can see this in the following example:
```
List<String> strings = List.of("one", "two", "three", "four", "five", "six");
Set<String> set = new HashSet<>();
set.addAll(strings);
set.forEach(System.out::println);
```
* Running this code will produce the following:
```
six
four
one
two
three
five
```
* Some implementations of Set give you the same order when you iterate over their elements, but since this is not guaranteed, your code should not rely on that.
##### Extending Set with SortedSet
* The first extension of Set is the SortedSet interface. The SortedSet interface keeps its elements sorted according to a certain comparison logic. The Collections Framework gives you one implementation of SortedSet, called TreeSet. 
* As you already saw, either you provide a comparator when you build a TreeSet, or you implement the Comparable interface for the elements you put in the TreeSet. If you do both, then the comparator takes precedence. 
* The SortedSet interface adds new methods to Set.
1. first() and last() returns the lowest and the largest elements of the set 
2. headSet(toElement) and tailSet(fromElement) returns you subsets containing the elements lower than toElement or greater than fromElement 
3. subSet(fromElement, toElement) gives you a subset of the element between fromElement and toElement.
* The toElement and fromElement do not have to be elements of the main set. If they are, then toElement is not included in the result and fromElement is, following the usual convention.
* Consider the following example:
```
SortedSet<String> strings = new TreeSet<>(Set.of("a", "b", "c", "d", "e", "f"));
SortedSet<String> subSet = strings.subSet("aa", "d");
System.out.println("sub set = " + subSet);

Running this code will give you the following:

sub set = [b, c]
```
* The three subsets that these methods return are views on the main set. No copy is made, meaning that any change you make to these subsets will be reflected in the set, and the other way round. 
* You can remove or add elements to the main set through these subsets. There is one point you need to keep in mind though. These three subsets remember the limits on which they have been built. For consistency reasons, it is not legal to add an element through a subset outside its limits. For instance, if you take a headSet and try to add an element greater than toElement, then you will get an IllegalArgumentException.
##### Extending SortedSet with NavigableSet
* Java SE 6 saw the introduction of an extension of SortedSet with the addition of more methods. It turns out that the TreeSet class was retrofitted to implement NavigableSet. So you can use the same class for both interfaces. 
* Some methods are overloaded by NavigableSet.
1. headSet(), tailSet(), and subSet() may take a further boolean arguments to specify whether the limits (toElement or fromElement) are to be included in the resulting subset.
* Other methods have been added.
1. ceiling(element), and floor(element) return the greatest element lesser or equal than, or the lowest element greater or equal than the provided element. If there is no such element then null is returned 
2. lower(element), and higher(element) return the greater element lesser than, or the lowest element greater than the provided element. If there is no such element then null is returned. 
3. pollFirst(), and pollLast() return and removes the lowest or the greatest element of the set.
* Furthermore, NavigableSet also allows you to iterate over its elements in descending order. There are two ways to do this.
1. You can call descendingIterator(): it gives you a regular Iterator that traverses the set in the descending order. 
2. You can also call descendingSet(). What you get in return is another NavigableSet that is a view on this set and that makes you think you have the same set, sorted in the reversed order.
* The following example demonstrates this.
```
NavigableSet<String> sortedStrings = new TreeSet<>(Set.of("a", "b", "c", "d", "e", "f"));
System.out.println("sorted strings = " + sortedStrings);
NavigableSet<String> reversedStrings = sortedStrings.descendingSet();
System.out.println("reversed strings = " + reversedStrings);
```
* Running this code will give you the following:
```
sorted strings = [a, b, c, d, e, f]
reversed strings = [f, e, d, c, b, a]
```

[The Collection FrameWork](./README.md) |  [Extending Collection with List](./Extending_Collection_with_List.md)| Extending Collection with Set, SortedSet and NavigableSet | [Creating and Processing Data with the Collections Factory Methods](./Creating_and_Processing_Data_with_the_Collections_Factory_Methods.md)