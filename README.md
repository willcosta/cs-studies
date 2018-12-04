# cs-studies
A bunch of stuff that I used to learn about computer science and algorithms.

## General Stuff

### big-O
BigO is an abstract way to measure the complexity of a function. It can be used as a measure for both time (how long does a function will take to complete) and space (how much memory it will use)
http://bigocheatsheet.com/

### Memoization
It's a way to store the result of a function so you don't have to execute it again. This is specially useful on recursions.
```js
function makeMemoFibo() {
  const memo = {};
  return fibo = (n) => {
    if(memo[n]) return memo[n];
    if(n <= 1) return 1;
    memo[n] = fibo(n - 1, memo) + fibo(n - 2, memo);
    return memo[n];
  }
}

const mFibo = makeMemoFibo();
for(let i = 0; i < 100; i++){
  console.log(i, mFibo(i));
}
```
The above example calculate the fibonacci at a given index its quite a expensive function as the index grows so we store
the result on the memo object. We use it as a closure so we don't polute the global scope with the memoization.

## Search

### Linear Search
You create a loop and check each item on the array until you find it
```js
function linearSearch(array, search) {
  for(let i = 0; i < array.length; i++) {
    const item = array[i];
    if(item === search){
      return i;
    }
  }
  return -1;
}

linearSearch([0, 2, 3, 4, 5, 1, 3], 1); // output: 5
```
big-O: O(n)

### Binary Search
When you a have a array that is already sorted and you have to find something inside this array instead of doing a linear search you can use a Binary search. It splits the array with each iteration and adjusts the min and max range depending on the proximity to what you are looking for. 

```js
function binarySearch(array, search) {
  let min = 0;
  let max = array.length - 1;
  while(min <= max) {
    let middle = Math.floor((min + max) / 2);
    let item = array[middle];
    if(item < search) {
      min = middle + 1;
    }else if(item > search) {
      max = middle - 1;
    }else{
      return middle;
    }
  }
  return -1;
}
```
big-O: O(log n)

## Sorting

### Bubble Sort

Make a pass on a array and if there is anything out of order swap then,
do it while you make a full pass on the array and you don't have to swap
anything

```js
const bubbleSort = (nums) => {
  const sorted = [].concat(nums);
  let swaped = true;
  while(swaped){
    swaped = false;
    for (let i = 0; i <= sorted.length; i++) {
      const currNum = sorted[i];
      const nextNum = sorted[i+1]
      if(currNum > nextNum){
        sorted[i] = nextNum;
        sorted[i+1] = currNum;
        swaped = true;
      }
    }
  }
  return sorted;
}
```

### Insertion Sort

You have two loops, the outer loop goes through the whole array from the second element,
the inner loop goes through the first element until the outer loop current position.
It checks both the current number and the next one, if its out of order it removes the next(i) 
element using splice and inserts it before the current one (j)

```js
const insertionSort = (nums) => {
  const sorted = [].concat(nums);
  
  for (let i = 1; i < sorted.length; i++) {
    for(let j = 0; j < i; j++){
      const current = sorted[j];
      const next = sorted[i];
      if(next < current){
        sorted.splice(i, 1);
        sorted.splice(j, 0, next);
      }
    }
  }
  return sorted;
}
```

### Merge Sort

```js
const mergeSort = (nums) => {
  if (nums.length < 2) {
    return nums;
  }
  
  const middle = Math.round(nums.length/2);
  const left = nums.slice(0, middle);
  const right = nums.slice(middle);

  return _mergeSortMerger(mergeSort(left), mergeSort(right));
}

const _mergeSortMerger = (left, right) => {
  const sorted = [];
  while(left.length && right.length){
    const l = left[0];
    const r = right[0];
    if(l < r){
      sorted.push(left.shift());
    }else{
      sorted.push(right.shift());
    }
  }

  return sorted.concat(left, right);
}
```
