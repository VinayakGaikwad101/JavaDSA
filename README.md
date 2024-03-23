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
int sum = a[0];
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
int sum = a[0];
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
int sum = a[0];
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
int sum = a[0];
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

