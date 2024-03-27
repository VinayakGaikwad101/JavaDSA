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

## 3) Primality Test: 
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

