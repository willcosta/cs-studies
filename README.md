# cs-studies
A bunch of stuff that I used to learn about computer science and algorithms.

## big-O
BigO is an abstract way to measure the complexity of a function. It can be used as a measure for both time (how long does a function will take to complete) and space (how much memory it will use)
http://bigocheatsheet.com/

## Memoization
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


## Linear Search
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

## Binary Search
When you a have a array that is already sorted and you have to find something inside this array instead of doing a linear search () 

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
