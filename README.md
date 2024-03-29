# JavaDSA
Important Algorithms and DS, and tips and tricks

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
