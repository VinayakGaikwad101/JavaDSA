# JavaDSA
Important Algorithms and DS, and tips and tricks

---
# DS:
---
## 1) LinkedList: 
### Main.java: 

```sh 
import java.util.*;
public class Main {
  public static void main(String[] args) {

    // Below is LL: 
    // Java's implementation of LL:
    LinkedList<Integer> ll = new LinkedList<>();
    ll.add(123);
    ll.add(23);
    ll.add(56);
    System.out.println("Built in LL: "+ ll); 

    // Our implementation of LL:
    LL ourll = new LL();
    // this initializes an empty LL, with size = 0, & head & tail

    ourll.insertFirst(42);
    ourll.insertFirst(23);
    ourll.insertFirst(56);

    System.out.println("Our implementation of LL: ");
    ourll.display(); // to display our ll

    ourll.insertFirst(88);
    System.out.println("Inserting 88 at the start: ");
    ourll.display();
    
    ourll.insertLast(33);
    System.out.println("Inserting 33 at the end: ");
    ourll.display();

    ourll.insert(44, 2);
    System.out.println("Inserting 44 at index 2: ");
    ourll.display();

    System.out.println("Deleting first element: "+       
    ourll.deleteFirst());
    ourll.display();

    System.out.println("Deleting last element: "+       
    ourll.deleteLast());
    ourll.display();

    System.out.println("Deleting element at index 1: "+       
    ourll.delete(1));
    ourll.display();

    int index = ourll.find(42);
    System.out.println("Element 42 found at index: "+ index);
    // Above is LL

    // Below is DLL
    DLL ourdll = new DLL();
    ourdll.insertFirst(42);
    ourdll.insertFirst(23);
    ourdll.insertFirst(56);
    System.out.println("Our implementation of DLL: ");
    ourdll.display();
    System.out.println("Reverse DLL: ");
    ourdll.displayRev();

    ourdll.insertLast(33);
    System.out.println("Inserting 33 at the end: ");
    ourdll.display();

    ourdll.insert(699, 2);
    System.out.println("Inserting 699 at 2 index: ");
    ourdll.display();

    ourdll.deleteFirst();
    System.out.println("Deleting first element: ");
    ourdll.display();

    ourdll.deleteLast();
    System.out.println("Deleting last element: ");
    ourdll.display();
    // Above is DLL

    // Below is CLL
    CLL ourcll = new CLL();
    ourcll.insert(42);
    ourcll.insert(23);
    ourcll.insert(56);
    ourcll.insert(88);
    System.out.println("Our implementation of CLL: ");
    ourcll.display();

    ourcll.delete(23);
    System.out.println("Deleting 23: ");
    ourcll.display();
    // Above is CLL
  }
}
```

### LL.java: 

```sh 
public class LL {
  // private because we dont want anyone to directly modify this class
  private Node head;
  private Node tail;
  private int size;

  public LL() {
    this.size = 0;
  }

  public void insertFirst(int val) {
    Node node = new Node(val);
    node.next = head;
    head = node;
    if(tail==null) { // for 1st element insertion
      tail = head;
    }
    size++;
  }

  public void insertLast(int val) {
    if(tail==null) {
      insertFirst(val);
      return;
    }
    Node node = new Node(val);
    tail.next = node;
    tail = node;
    size++;
  }

  public void insert(int val, int index) {
    if(index==0) {
      insertFirst(val);
      return;
    }
    if(index == size) {
      insertLast(val);
      return;
    }
    Node temp = head;
    for(int i=1; i<index; i++) {
      temp = temp.next;
    }
    Node node = new Node(val, temp.next);
    temp.next = node;
    size++;
  }

  public int deleteLast() {
    if(size<=1) {
      return deleteFirst();
    }
    Node secondLast = get(size-2);
    int val = tail.value;
    tail = secondLast;
    tail.next = null;
    size--;
    return val;
  }

  public int delete(int index) {
    if(index == 0) {
      return deleteFirst();
    }
    if(index == size-1) {
      return deleteLast();
    }
    Node prev = get(index - 1);
    int val = prev.next.value;
    prev.next = prev.next.next;
    size--;
    return val;
  }
  
  public int find(int value) {
      Node node = head;
      int index = 0;
      while (node != null) {
          if (node.value == value) {
              return index;
          }
          node = node.next;
          index++;
      }
      return -1; // Not found
  }
  
  public Node get(int index) {
    Node node = head;
    for(int i = 0; i<index; i++) {
      node = node.next;
    }
    return node;
  }
  
  public int deleteFirst() {
    int val = head.value;
    head = head.next;
    if(head==null) {
      tail = null;
    }
    size--;
    return val;
  }
  
  public void display() {
    Node temp = head;
    while(temp!=null) {
      System.out.print(temp.value + " -> ");
      temp = temp.next;
    }
    System.out.println("NULL");
  }

  private class Node {
    private int value;
    private Node next;
    public Node(int value) {
      this.value = value;
    }
    public Node(int value, Node next) {
      this.value = value;
      this.next = next;
    }
  }
}
```

### DLL.java: 

```sh 
public class DLL {

  private Node head;
  int size = 0; 
  
  public void insertFirst(int val) {
    Node node = new Node(val);
    node.next = head;
    node.prev = null;
    if(head!=null) {
      head.prev = node;
    }
    head = node;
    size++;
  } 

  public void display() {
    Node node = head;
    System.out.print("NULL <=> ");
    while (node != null) {
      System.out.print(node.val + " <=> ");
      node = node.next;
    }
    System.out.println("NULL");
  }

  public void displayRev() {
    Node last = head;
    if (last == null) {
      System.out.println("NULL");
      return;
    }

    while (last.next != null) {
      last = last.next;
    }
    System.out.print("NULL <=> ");
    while (last != null) {
      System.out.print(last.val + " <=> ");
      last = last.prev;
    }
    System.out.println("NULL");
  }

  public void insertLast(int val) {
    Node node = new Node(val);
    Node last = head;

    node.next = null;
    
    if(head==null) {
      node.prev = null;
      head = node;
      return;
    }
      
    while(last.next!=null) {
      last = last.next;
    }

    last.next = node;
    node.prev = last;
    
  }

  public void insert(int val, int index) {
    if (index < 0 || index > size) {
      throw new IndexOutOfBoundsException("Invalid index: " + index);
    }

    if (index == 0) {
      insertFirst(val);
      return;
    }

    if (index == size) {
      insertLast(val);
      return;
    }

    Node current = head;
    for (int i = 0; i < index - 1; i++) {
      current = current.next;
    }

    Node newNode = new Node(val);

    newNode.next = current.next;
    current.next.prev = newNode;
    newNode.prev = current;
    current.next = newNode;

    size++;
  }

  public int deleteFirst() {
    if (head == null) {
      return -1;
    }

    int val = head.val;
    head = head.next;
    if (head != null) {
      head.prev = null;
    } else {
    }
    size--;
    return val;
  }

  public int deleteLast() {
    if (head == null) {
      return -1;
    }

    if (head.next == null) {
      int val = head.val;
      head = null;
      size--;
      return val;
    }

    Node last = head;
    while (last.next.next != null) {
      last = last.next;
    }

    int val = last.next.val;
    last.next = null;
    size--;
    return val;
  }
  
  private class Node {
    int val;
    Node next;
    Node prev;

  public Node(int val) {
    this.val = val;
    }

  public Node(int val, Node next, Node prev) {
    this.val = val;
    this.next = next;
    this.prev = prev;
    }
  }
}
```

### CLL.java: 

```sh 
public class CLL {

  private Node head;
  private Node tail;

  public CLL() {
    this.head = null;
    this.tail = null;
  }

  public void insert(int val) {
    Node node = new Node(val);
    if(head==null) {
      head = node;
      tail = node;
      return;
    }
    tail.next = node;
    node.next = head;
    tail = node;
  }

  public void display() {
    Node node = head;
    if(head!=null) {
      do {
        System.out.print(node.val + " -> ");
        node = node.next;
      } while(node!=head);
    }
    System.out.println("END");
  }

  public void delete(int val) {
    Node node = head;
    if(node==null) {
      return;
    }
    if(node.val==val) {
      head = head.next;
      tail.next = head;
      return;
    }
    do {
      Node n = node.next;
      if(n.val==val) {
        node.next = n.next;
        break;
      }
      node = node.next;
    } while(node!=head);
  }
  
  private class Node {
    int val;
    Node next;

    public Node(int val) {
      this.val = val;
    }

    
  }
}
```

### DLL.java: 
Output:
```sh 
Built in LL: [123, 23, 56]
Our implementation of LL: 
56 -> 23 -> 42 -> NULL
Inserting 88 at the start: 
88 -> 56 -> 23 -> 42 -> NULL
Inserting 33 at the end: 
88 -> 56 -> 23 -> 42 -> 33 -> NULL
Inserting 44 at index 2: 
88 -> 56 -> 44 -> 23 -> 42 -> 33 -> NULL
Deleting first element: 88
56 -> 44 -> 23 -> 42 -> 33 -> NULL
Deleting last element: 33
56 -> 44 -> 23 -> 42 -> NULL
Deleting element at index 1: 44
56 -> 23 -> 42 -> NULL
Element 42 found at index: 2
Our implementation of DLL: 
NULL <=> 56 <=> 23 <=> 42 <=> NULL
Reverse DLL: 
NULL <=> 42 <=> 23 <=> 56 <=> NULL
Inserting 33 at the end: 
NULL <=> 56 <=> 23 <=> 42 <=> 33 <=> NULL
Inserting 699 at 2 index: 
NULL <=> 56 <=> 23 <=> 699 <=> 42 <=> 33 <=> NULL
Deleting first element: 
NULL <=> 23 <=> 699 <=> 42 <=> 33 <=> NULL
Deleting last element: 
NULL <=> 23 <=> 699 <=> 42 <=> NULL
Our implementation of CLL: 
42 -> 23 -> 56 -> 88 -> END
Deleting 23: 
42 -> 56 -> 88 -> END
```

---


# Important Algorithms:

## 1) Kadane's Algorithm: 
### Used to find the minimum / maximum sum of a contiguous subarray

[Link for reference](https://youtu.be/Qd_qhRsSays?si=NiV8ncUylh8pBVxx)
### has 4 variants:
### 1. Finding maximum contiguous subarray sum (subarray cant be empty):
```sh
int[] a = new int[n]; // assume our array of length = n
int maxSum = a[0]; // this will be the maxSum
int sum = 0;
for(int i = 0; i<n; i++) {
    if(sum>=0) {
        sum += a[i];
    }
    else {
        sum = a[i];
    }
    maxSum = Math.max(sum, maxSum);
}
```

### 2. Finding maximum contiguous subarray sum (subarray can be empty if maxSum is negative):
```sh
int[] a = new int[n]; // assume our array of length = n
int maxSum = a[0]; // this will be the maxSum
int sum = 0;
for(int i = 0; i<n; i++) {
    if(sum>=0) {
        sum += a[i];
    }
    else {
        sum = a[i];
    }
    maxSum = Math.max(sum, maxSum);
}
if(maxSum<0) {
    maxSum = 0;
}
```

### 3. Finding minimum contiguous subarray sum (subarray cant be empty):
```sh
int[] a = new int[n]; // assume our array of length = n
int minSum = a[0]; // this will be the minSum
int sum = 0;
for(int i = 0; i<n; i++) {
    if(sum>=0) {
        sum += a[i];
    }
    else {
        sum = a[i];
    }
    minSum = Math.min(sum, minSum);
}
```

### 4. Finding minimum contiguous subarray sum (subarray can be empty if minSum is negative):
```sh
int[] a = new int[n]; // assume our array of length = n
int minSum = a[0]; // this will be the minSum
int sum = 0;
for(int i = 0; i<n; i++) {
    if(sum>=0) {
        sum += a[i];
    }
    else {
        sum = a[i];
    }
    minSum = Math.min(sum, minSum);
}
if(minSum<0) {
    minSum = 0;
}
```

---

## 2) Boyer Moore's Majority Voting Algorithm: 
### Used to find element of maximum occurrence in an array

[Link for reference](https://youtu.be/X0G5jEcvroo?si=JrS8J9kEeaujLlQz)
### has only 1 variant:
### 1. Finding the maximum occurring element in an array:
element is majority occuring, if it's occurrence>n/2

```sh 
int[] a = new int[n]; //assume array of length n, unsorted/sorted array
int ansIndex = 0;
int count = 1;
for(int i = 1; i<n; i++) {
    if(a[i]==a[ansIndex]) {
        count++;
    }
    else {
        count--;
    }
    if(count==0) {
        ansIndex = i;
        count = 1;
    }
}

// now ansIndex is the index of maximum occurring element
// check if the answer is actually majority element (unnecessary)
int countofMax = 0;
boolean isMax = false;
for(int i = 0; i<n; i++) {
    if(a[i]==a[ansIndex]) {
        countOfMax++;
    }
}
if(count>n/2) {
    isMax = true;
}
else {
    isMax = false;
}
```

---
# Number Theory:
---

## 1) Primality Test: 
### Used to find if a number is prime or not

[Link for reference](https://youtu.be/toT21DALrCg?si=k2_2bHPeWWASTOXE)
### has only 1 variant:
### 1. Time complexity: O(√N):
Normal check: i=2 to n-1, but reduced: i=2 to √n

```sh 
bool isPrime(int n) {
    if(n==1) {
        return false;
    }
    for(int i = 2; i*i<=n; i++) {
    // checking till √n as above condition also means i<=√n
    if(n%i == 0) {
        return false;
    }
    return true;
}
```

---

## 2) Sieve of Eratosthenes: 
### Used to generate Prime Numbers in a given range [1, n]

[Link for reference](https://youtu.be/7zYMjXqdchc?si=a-B3nOE5hcjfTzda)
### has only 1 variant:
### 1. Time complexity: O(N*log(log N)):
Similar to Primality Test, we check for i<=√n, and cross out all multiples of 2, then 3, then 5 and so on.
But for 5 and above, we start the check from it's square, as 10, 15 and 20 would've been already marked out as composite due to 2 and 3.
Similarly, for 7 (7²=49), (11²=121), etc. 

```sh 
import java.util.*;
public class main {
	  public static List<Integer> findPrimes(int low, int high) { // returns an Integer List, hence the return datatype
	    int n = high + 1; // Adjust size for inclusivity
	    boolean[] isPrime = new boolean[n]; // boolean array called isPrime
	    Arrays.fill(isPrime, true); // fill isPrime array with true (assume all are Prime)
	    isPrime[0] = isPrime[1] = false; // set 0 and 1 as not prime (false)

	    for (int i = 2; i * i < n; i++) { // loop from i to √n, refer to Primality Test for more info on why from i to √n
	      if (isPrime[i]) { // if a number is prime, enter this 
	        for (int j = i * i; j < n; j += i) { // marks all multiples of i starting from i² to n as false because all of its previous elements are marked as composite by default
	          isPrime[j] = false; // mark as not prime / composite
	        }
	      }
	    }

	    List<Integer> primes = new ArrayList<>(); // make a new List that will store our Primes from low to high
	    for (int i = Math.max(low, 2); i <= high; i++) { // Handle negative low 
	      if (isPrime[i]) { // if it is prime, then add to primes List
	        primes.add(i);
	      }
	    }
	    return primes; // return primes List
	  }

	  public static void main(String[] args) {
	    int low = -9999; // set this as the lowerBound (included)
	    int high = 100; // set this as the upperBound (included)
	    List<Integer> primes = findPrimes(low, high); // List variable to hold all primes

           //Unnecessary:
	    System.out.println("Prime numbers between " + low + " and " + high + ":");
	    for (int prime : primes) { // iteration to print all elements of primes List
	      System.out.print(prime + " ");
	    }
	  }
}

// primes is an ArrayList that contains all Primes within [low, high] (inclusive) 
```

---

## 3) Prime Factorization: 
### Gives Prime Factors of a number

[Link for reference](https://youtu.be/UZJ2nO_rTPg?si=B5zyrAYhFuPwK7LJ)
### has only 1 variant:
### 1. Time complexity: O(√N):

```sh

import java.util.Scanner;
public class main {
	public static void primeFactor(int N) { // take integer input
		  for (int i = 2; i <= N; i++) { // loop from [2,N]
		    if (N % i == 0) { // if N is divisible by i, means i is a factor, enter
		      int power = 0; // set power = 0 for each i
		      while (N % i == 0) { // as long as N is divisible by i
		        power++; // increment power by 1
		        N /= i; // then divide N by i and again while N%i==0 enter again 
		      }
		      System.out.print(i + "^" + power + " "); // Use print for spacing
		    }
		  }
		}


    public static void main(String[] args) {
    	int n = 123;
    	primeFactor(n);
    }
}

```

---

## 4) Binary Exponentiation: 
### Technique to calculate a^n in O(log N) time

[Link for reference](https://youtu.be/lsdwBlk9YGI?si=niETJ9XC7detgE82)
### has only 1 variant:
### 1. Time complexity: O(log N):
works on the principle that to calculate a^n, we can square a and half its power, which essentially gives us (a^2)^(n/2) = a^n as 2/2=1
so we repeat this step as long as the power is even, as soon as it is odd, we can calculate a^n faster
Basic Principle: while base is even, square the base and divide the power by 2, else give a^n

Also, keep a variable res = 1. As soon as the power (n) is odd, we reduce power by 1, ie, (n-1) and res*=a.
As soon as power becomes 0, we return res

```sh

	int binaryExponentiation(int a, int pow) {
		int res = 1;
		while(pow!=0) {
			if(pow%2!=0) {
				res*=a;
				pow--;
			}
			else {
				a*=a;
				pow/=2;
			}
		}
		return res;
	}

```

---

## 5) Modular Exponentiation: 
### Technique to calculate a^n % p in O(log N) time

[Link for reference](https://youtu.be/lsdwBlk9YGI?si=niETJ9XC7detgE82)
### has only 1 variant:
### 1. Time complexity: O(log N):
works same as Binary Exponentiation ( 4 )

```sh

	int binaryExponentiation(int a, int pow, int p) {
		int res = 1;
		while(pow!=0) {
			if(pow%2!=0) {
				res*=a%p;
				pow--;
			}
			else {
				a*=a%p;
				pow/=2;
			}
		}
		return res;
	}

```
