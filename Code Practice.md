// LRU Cache in js

// console.log("Logs are running...")

// class LRUCache {
//   constructor(bucket) {
//     this.bucket = bucket
//     this.data = new Map();
//   }

//   get(item) {
//     let isItemPresent = this.data.get(item);
//     if (!isItemPresent) {
//       return -1;
//     }

//     // First delete occurence and put it on the front;
//     this.data.delete(item);
//     this.data.set(item, isItemPresent)

//   }

//   put(item, value) {
//     console.log("Put is running")
//     let isItemPresent = this.data.get(item)
//     if (isItemPresent) {
//       // First delete the item and makr it has the latest usage
//       this.data.delete(item);
//       // Set the Item Again to it
//       this.data.set(item,value);
//       return "success";
//     } else {
//       this.data.set(item,value);

//       // Refine the bucket if it goes beyond size
//       if (this.data.size > this.bucket) {
//         // delete the last used key
//         const lastUsedKey = this.data.keys().next().value;
//         console.log("LAST USED KEY >>", lastUsedKey);
//         this.data.delete(lastUsedKey);
//       }
//     }
//   }
// }

// const c1 = new LRUCache(2)
// c1.put(1,1);
// c1.put(2,2);
// c1.put(3,3);


// Custom Deep CLone Method

// const input = {
//   name: "A",
//   age: 30,
//   isActive: true,
//   // scores: [10, 20, 30],
//   meta: {
//     createdAt: "2024-01-01",
//     tags: ["js", "frontend"]
//   }
// };

// function deepClone(data) {
//   if (data===null || typeof data!=='object') {
//     return data;
//   }

//   if(Array.isArray(data)) {
//     return data.map(it => deepClone(it))
//   }

//   let result = {};
//   for(const item in data) {
//     result[item] = deepClone(data[item])
//   }


//   return result;
// }

// const res = deepClone(input)
// // console.log({res})

// function userPath(data, path='user', store = {}) {
//   if(data===null || typeof data!=='object') {
//     store[path] = data;
//     return;
//   }

//   if (Array.isArray(data)) {
//     data.forEach((it, index) => {
//       let pathForArray = `${path}.${index}`;
//       store[pathForArray] = userPath(it, pathForArray, store)
//     })
//     return;
//   }

//   for(const key in data) {
//     let generateSuffix = path ? `${path}.${key}` : `${key}`;

//     userPath(data[key], generateSuffix, store)
//   }

//   return store
// }

// const res2 = userPath(input)
// console.log({res2})

// Currying

// variable number of arguments
// function sum(...args) {

//   return function(...next) {
//     if (!next.length) {
//       return args.reduce((acc, cumm) => acc+=cumm, 0);
//     }

//     return sum(...args, ...next)
//   }
// }

// const res = sum(1,2,3)(4,1)(5)();
// console.log({res})

// we will use the concept of closure
// function sum(a) {
//   let total = a;

//   function inner(b) {
//     if(b===undefined) {
//       return total;
//     }
//     total+=b;
//     return inner
//   }

//   return inner
// }



// const res = sum(1)(2)(3)();
// console.log({res})


// Custom My Bind

// Function.prototype.myBind = function(originalFn, ...args) {
//   let fnThis = originalFn;

//   return function() {
//       return fnThis.call(...args)
//   }
// }


// GROUP ANAGRAMS


// const arr = ["eat", "tea", "tan", "ate", "nat", "bat"];

// // Another solution is to create a hash key firstly, then move ahead
// function groupAnagrams(data) {
//   let obj = {}

//   for(let i=0; i<arr.length; i++) {
//     const word = arr[i].split('').sort().join('')
    
//     if (!obj[word]) {
//       obj[word] = [arr[i]]
//     } else {
//       obj[word].push(arr[i]);
//     }
  
//   }


//   return Object.values(obj)
// }

// const result = groupAnagrams(arr)
// console.log({result})

// Valid Parenthesis

// const item = "()[]{}";

// function validParenthesis(data) {
//   // If no data was there, base check
//   if(!data) {
//     return false;
//   }

//   // configure a stack
//   let stack = [];

//   // Looping over string and check the result
//   for(let i=0; i<data.length; i++) {
//     let bracket = data[i];

//     if (bracket === '(' || bracket === '[' || bracket==='{') {
//       stack.push(bracket);
//     } else {
//       const poppedElement = stack.pop();

//       if (!poppedElement) {
//         return false;
//       }

//       if(bracket===')' && poppedElement!=='(') {
//         return false;
//       } else if(bracket===']' && poppedElement!=='[') {
//         return false;
//       } else if(bracket==='}' && poppedElement!=='{') {
//         return false;
//       }
//     }
//   }

//   if (stack.length) {
//     return false;
//   }

//   return true;
// }

// const res = validParenthesis(item)
// console.log({res})


// Deep cloning

// const obj = {
//   name: "Ganesh",
//   a: undefined
//   // abc: function() {
//   //   console.log(this)
//   // }
// }

// const res = JSON.parse(JSON.stringify(obj))

// console.log({res})


// Product of Array except self

// const arr = [-1,1,0,-3,3]

// function selfProduct(data) {
//   let result = new Array({length: data.length})

//   let allProduct = data.reduce((acc, cumm) => acc*=cumm, 1)
//   console.log({allProduct})
//   for(let i=0; i<data.length; i++) {
//     const toStore = allProduct/data[i]
//     result[i] = toStore === 0 ? 0 : toStore;
//   }

//   console.log({result})
// }

// selfProduct(arr)

// THIS
// "use strict"

// function xyz() {

  
//   const student = {
//     name: "Ganesh",
//     printName: {
//       x: () => {
//         console.log(this)
//       }
//     }
//   }
  
//   student.printName.x()
  
// }

// xyz()
// LRU Cache Implementation
// LRU - Least recently used Cache

// const SIZE_LIMIT=2
// class LRUCache {

//   constructor(capacity) {
//     this.capacity = capacity
//     this.cache = new Map(); // Ignoring Bucket for now
//   }

//   getMap() {
//     console.log("Map >>", this.cache)
//   }

//   get(itemKey) {
//     if (!this.cache.has(itemKey)) {
//       return -1;
//     }
//     // Get the key first, delete the entry and put it in front
//     let storeKeyVal = this.cache.get(itemKey);
//     this.cache.delete(itemKey);

//     // Put back again so that it remains in order
//     this.cache.set(itemKey, storeKeyVal);

//     return storeKeyVal;
//   }

//   put(itemKey, val) {
//     // Get the Key First
//     if (this.cache.has(itemKey)) {
//       this.cache.delete(itemKey)
//     }

//     this.cache.set(itemKey, val);

//     // If size of cache is full, delete the item first
//     // console.log(this.cache.size)
//     if (this.cache.size>this.capacity) {
//       const keyToBeRemoved = this.cache.keys().next().value;
//       this.cache.delete(keyToBeRemoved);
//     }
  
//     return val;
//   }

// }

// const cache = new LRUCache(2);

// cache.put(1, 1);
// console.log('1st >>', cache.getMap())
// cache.put(2, 2);
// console.log('2nd >>', cache.getMap())
// cache.get(1); // returns 1
// console.log('3rd >>', cache.getMap())
// cache.put(3, 3); // evicts key 2
// console.log('4th >>', cache.getMap())
// cache.get(2); // returns -1
// console.log('5th >>', cache.getMap())


// console.log({cache})

// function deepEqual(a, b) {
//   // 1. Strict equality (handles primitives + same reference)
//   if (a === b) return true;

//   // 2. Handle null
//   if (a === null || b === null) return false;

//   // 3. Type check
//   if (typeof a !== "object" || typeof b !== "object") {
//     return false;
//   }

//   // 4. Array check
//   if (Array.isArray(a) !== Array.isArray(b)) return false;

//   // 5. Compare keys length
//   const keysA = Object.keys(a);
//   const keysB = Object.keys(b);

//   if (keysA.length !== keysB.length) return false;

//   // 6. Recursive check
//   for (let key of keysA) {
//     if (!keysB.includes(key)) return false;

//     if (!deepEqual(a[key], b[key])) {
//       return false;
//     }
//   }

//   return true;
// }


// const res = deepEqual(
//   { a: 1, b: { c: 2 } },
//   { a: 1, b: { c: 2 } }
// )


// console.log({res})

// Deep cloning of an object

// const originalObject = {
//   name: "DeepCloneDemo",
//   id: 1,
//   details: {
//     created: "2026-04-22",
//     tags: ["test", "clone", "nested"],
//     metadata: {
//       active: true,
//       count: 10
//     }
//   }
// };

// // We will use the concept of recursion over here
// function deepClone(data) {
//   // Add the base conditions
//   if (data === null || typeof data!=='object') {
//     return data;
//   }

//   if(Array.isArray(data)) {
//     return data.map(deepClone)
//   }

//   let temp = {}
//   for(const key in data) {
//     temp[key] = deepClone(data[key])
//   }

//   return temp;
// }

// const result = deepClone(originalObject)
// console.log({result})

// const transactions = [
//   { userId: 1, amount: 100, type: "credit" },
//   { userId: 2, amount: 50, type: "debit" },
//   { userId: 1, amount: 200, type: "credit" },
//   { userId: 2, amount: 30, type: "credit" },
//   { userId: 1, amount: 50, type: "debit" }
// ];

// function netBalance(data) {
//   let res = {};

//   transactions.forEach((item, index) => {
//     if (!res[item.userId]) {
//       res[item.userId] = 0
//     }

//     if (item.type==='credit') {
//       res[item.userId] = res[item.userId] + item.amount
//     } else {
//       res[item.userId] = res[item.userId] - item.amount
//     }
//   })

//   console.log({res})
// }

// const res = netBalance(transactions)

// Flattening of an array

// let arr = [1,2,[3,4,[5,6]]];

// function flatten(data, flatt, store=[]) {

//   for(let i=0; i<data.length; i++) {
//     if(Array.isArray(data[i]) && flatt>0) {
//       flatten(data[i], flatt-1, store)
//     } else {
//       store.push(data[i])
//     }
//   }
//   return store;
// }

// const res = flatten(arr, 1);
// console.log({res})


// Debounce Behaviour
// const fn = () => console.log("API call");

// function debounce(mainFun, delay) {
//   let timer=null;

//   return (...args) => {
//     clearTimeout(timer)
//     timer=setTimeout(() => {
//       mainFun(...args)
//     }, delay)
//   }
// }


// // considering that it doesn't have any argument being passed to it
// const debounced = debounce(fn, 500);

// debounced();
// debounced();
// debounced();

// Flattening of deeply nested Array

// const obj = {
//   a: 1,
//   b: {
//     c: 2,
//     d: {
//       e: [12,13,14,15]
//     }
//   },
//   f: 4
// };

// function deeplyNestedObjectFlattening(data, path="", store={}) {
//   if (typeof data!=='object' && !Array.isArray(data)) {
//     store[path] = data;
//   } else if (typeof data==='object' && Array.isArray(data)) {
//     data.forEach((item, index) => {
//       deeplyNestedObjectFlattening(item, `${path}.${index}`, store)
//     })
//     return
//   }
  
//   for(const key in data) {
//     const prefix = path ? (path + '.' + `${key}`) : `${key}`
//     deeplyNestedObjectFlattening(data[key], prefix, store)
//   }

//   return store;
// }

// const res = deeplyNestedObjectFlattening(obj)
// console.log({res})


// Group By Age

// const users = [
//   { id: 1, name: "A", age: 20 },
//   { id: 2, name: "B", age: 30 },
//   { id: 3, name: "C", age: 20 },
//   { id: 4, name: "D", age: 30 },
//   { id: 5, name: "E", age: 40 }
// ];

// function groupByAge(data) {
//   let res = {}

//   users.forEach((item) => {
//     if (!res[item.age]) {
//       res[item.age] = [item]
//     } else {
//       res[item.age].push(item)
//     }
//   })

//   console.log({res})
// } 

// groupByAge(users)


// Rotate Array In-place


// rotate([1,2,3,4,5], 2)
/**
 * Full Reversal -> [5,4,3,2,1]
 * Reverse the first 2 elements
 * Reverse the remaining elements
 */
// let arr = [1,2,3,4,5]


// function reverse(data, startIndex, endIndex) {
//   let low=startIndex;
//   let high=endIndex;

//   while(low<=high) {
//     // we can solve it by using a temporary variable, instead of using the js array destructuring
//     [data[low], data[high]] = [data[high], data[low]]
//     low++
//     high--;
//   }
// }

// function rotate(data, time) {
//   let totalNumberTimeToRotate = time%data?.length
//   reverse(data, 0, data.length-1)
//   reverse(data, 0, totalNumberTimeToRotate-1)
//   reverse(data, totalNumberTimeToRotate, data.length-1)
// }

// rotate(arr, 2)
// console.log({arr})

// Reverse a string and make the first letter capital

// const str = 'hello world';
// // output -> olleH dlroW;

// function getReversedWord(data) {
//   let str = '';

//   for (let i = data.length - 1; i >= 0; i--) {
//     if (i === 0) {
//       const capitaliseLetter = data[i].toUpperCase()
//       str += capitaliseLetter
//     } else {
//       str += data[i];
//     }

//   }
//   return str;
// }

// function reverseString(data) {
//   let finalString = '';

//   let currentWord = '';

//   for (let i = 0; i < data.length; i++) {
//     const ch = data[i];

//     if (ch !== ' ') {
//       currentWord += ch
//     } else {
//       if (finalString.length > 0) {
//         finalString += ' '
//       }

//       // Reverse the word and store it in finalString
//       let reversedWord = getReversedWord(currentWord)
//       finalString += reversedWord;
//       currentWord = ''
//     }
//   }

//   // HANDLE THE LAST WORD GRACEFULLY
//   if (currentWord.length > 0) {
//     if (finalString.length > 0) {
//       finalString += ' '
//     }

//     // Reverse the word and store it in finalString
//     let reversedWord = getReversedWord(currentWord)
//     finalString += reversedWord;
//   }

//   return finalString;
// }

// const res = reverseString(str)
// console.log({ res })



// Find the smallest word in a sentence;

// const str = "F the smallest word in aaaa bulll";

// function findSmallestWord(data) {
//   let smallestWord;
//   let currentWord = '';

//   for(let i=0; i<data.length; i++) {
//     const ch = data[i];
//     if (ch===' ') {
//       if(currentWord.length>0 && ( !smallestWord ? true : currentWord.length<smallestWord.length)) {
//         smallestWord=currentWord;
//       }
//       currentWord=''
//     } else {
//       currentWord+=ch
//     }
//   }

//   if (currentWord.length>0 && (!smallestWord || ( currentWord.length<smallestWord.length ))) {
//     smallestWord = currentWord
//   }

//   return smallestWord;
// }

// const res = findSmallestWord(str);
// console.log({res})



// Array Flattening

// const arrFlatten = (arr, depth) => {
//   let result = [];

//   const flatten = (data, dep) => {
//     for(let i=0; i<data.length; i++) {
//       if (!Array.isArray(data[i])) {
//         result.push(data[i])
//       } else {
//         if (dep>0) {
//           flatten(data[i], dep-1)
//         } else {
//           result.push(data[i])
//         }
//       }
//     }
//   }

//   flatten(arr, depth)

//   return result;
// }

// const nested = [1, [2, [3, [4]]]];
// const res = arrFlatten(nested, 2)
// console.log({res})

// Create Bank Account

// function bankAccount(initialValue) {
//   let amount=initialValue;

//   return {
//     deposit: function (amt) {
//       if (amount>=0) {
//         amount+=amt;
//         return amount;
//       }
//     },
//     withdraw: function(x) {
//       if (amount > 0 && amount>=x) {
//         amount-=x;
//         return amount;
//       }
//       return "Insufficent Amount";
//     },
//     getBalance: function() {
//       return amount;
//     }
//   }
// }


// console.log(typeof a); 
// var a = 1;
// function a() {}

// // Template String Parser

// const template = 'Hello, {{user.name}}! You have {{count}} messages.';
// const data = {
//   user: { name: 'Alice', email: 'alice@example.com' },
//   count: 5
// };

// function parseTemplate(template, data) {

// }

// parseTemplate(template, data);

// AWAIT WITH RETRIES

// async function fetchWithRetry(apiEndPoint, options) {
//   const {  }  
// }


// async function fetchWithRetries() {
//   const data = await fetchWithRetry('https://api.example.com/data', {
//     maxRetries: 3,
//     baseDelay: 1000
//   });

//   console.log({data})
// }

// fetchWithRetries()


// Two sum
// two cases -> Sorted Array or Unsorted Array
/**
 * {
 *  2: 0
 * 
 * }
 */

// const nums = [2, 7, 11, 15];
// const target = 18;

// function twoSum(arr, target) {
//   let mpp = {};

//   for(let i=0; i<arr.length; i++) {
//     const diff = target-arr[i]; // 2
//     if (mpp[diff] !== 'undefined') {
//       return [mpp[diff], i];
//     }
//     mpp[arr[i]] = i
//   }
// }

/**
 * 
 */

// const res = twoSum(nums, target)
// console.log({res})


// const userOne = { name: "Ganesh" }
// const userTwo = { ...userOne }

// userTwo.name = "Vidhi"
// console.log(" 1 >>", userOne.name)
// console.log(" 2 >>", userTwo.name)



// let word = "HELLO__WORLDS_"

// function longestLength(data) {
//   let largestLength=0;
//   let maxLength = 0

//   for(let i=0; i<data.length; i++) {
//     let character = data.charAt(i);

//     if (character==='_') {
//       largestLength=0;
//     } else {
//       largestLength+=1;
//       maxLength = Math.max(maxLength, largestLength);
//     }
//   }

//   console.log({maxLength})
//   return maxLength
// }

// const res = longestLength(word)
// console.log({res})

// Move all zeroes to end

// const data = [1,0,9,0,7,8,0,0,34]

// function moveZeroesToEnd(data) {
//   let pointer = 0;

//   for(let i=0; i<data.length; i++) {
//     if (data[i]!==0) {
//       data[pointer]=data[i];
//       pointer++
//     }
//   }

//   while(pointer<data.length) {
//     data[pointer] = 0;
//     pointer++;
//   }

//   return data
// }

// const res = moveZeroesToEnd(data);
// console.log({res})


// Merge Two Sorted Arrays

// const nums1 = [1,2,3, 0, 0, 0]
// const m = 3

// const nums2 = [2,5,6]
// const n = 3

// function mergeSortedArrays(dc1, dc2){
//   let i=0;
//   let j=0;
//   let result = [];
//   let track=0

//   while(i<dc1.length && j<dc2.length) {
//     if (dc1[i]<dc2[j]) {
//       dc1[track] = dc1[i];
//       i++;
//     } else {
//       dc1[track] = dc2[j]
//       j++;
//     }
//     track++
//   }

//   // while(i<dc1.length) {
//   //   result.push(dc1[i])
//   //   i++
//   // }

//   // while(j<dc2.length) {
//   //   result.push(dc2[j])
//   //   j++
//   // }

//   console.log({result})
// }

// const res = mergeSortedArrays(nums1, nums2)
// console.log({res})


// // Best Time to Buy and sell Stocks

// const prices = [7,1,5,3,6,4];

// function bestTimeToBuyAndSell(data) {
//   let maxProfit = 0;
//   let minPrice = data[0];

//   for(let i=1; i<data.length; i++) {
//     let profit = data[i]-minPrice;

//     if (profit>maxProfit) {
//       maxProfit = profit;
//     }

//     if (data[i]<minPrice) {
//       minPrice=data[i]
//     }
//   }

//   return maxProfit;
// }

// const res = bestTimeToBuyAndSell(prices)
// console.log({res})


// console.log("Hello")

// const arr = [0,0,1,1,1,2,3,3,3,4];

// function removeDuplicates(data) {
//   let pointer=0;
//   let arrSize=data.length;

//   for(let i=0; i<data.length; i++) {
//     if(arr[i]>arr[pointer]) {
//       pointer++;
//       arr[pointer] = arr[i]
//     }
//   }

//   console.log({data})

// }


// removeDuplicates(arr)

// All Promise Custom handlers

// const p1 = Promise.resolve(34);
// const p2 = new Promise((res, rej) => setTimeout(() => rej('P2 Resolved'), 2000))
// const p3 = Promise.reject(404);


// // Promise.allSettled
// // Promise.race - it returns me the first response, whether it is fail or pass

// function customPromiseRace(iterablePromises) {
//   return new Promise((res, rej) => {
//     iterablePromises.forEach((item) => {
//       Promise.resolve(item).then((data) => {
//         return res(data)
//       }).catch((err) => {
//         return rej(err)
//       })
//     })
//   })
// }

// customPromiseRace([p1, p2, p3]).then(data => console.log({data}))

// Promise.any - First fulfilled promise, if not return the aggregate errors
 
// function customPromiseAny(iterablePromises) {
//   return new Promise((res, rej) => {
//     let aggregateErrors = [];
//     let unresolved = iterablePromises.length

//     if (!iterablePromises || iterablePromises.length<1) {
//       return rej(aggregateErrors);
//     }

//     iterablePromises.forEach((item, index) => {
//       Promise.resolve(item).then((val) => {
//         return res(val)
//       }).catch((err) => {
//         aggregateErrors[index] = err;
//       }).finally(() => {
//         unresolved--;
//         if (unresolved===0) {
//           return rej(aggregateErrors)
//         }
//       })
//     })
//   })
// }

// customPromiseAny([p1, p2, p3]).then(data => console.log({data}))



// Promise.all

// function custtomPromiseAll(iterablePromises) {
//   return new Promise((res, rej) => {
//     if (!iterablePromises || iterablePromises.length<1) {
//       return res([]);
//     }
    
//     let result = new Array(iterablePromises.length);
//     let unresolved = iterablePromises.length
    
//     iterablePromises.forEach((item, index) => {
//       Promise.resolve(item).then((resolvedValue) => {
//         result[index] = resolvedValue
//         unresolved--
//         if (unresolved===0) {
//           return res(result);
//         }
//       }).catch((err) => {
//         return rej(err)
//       })
//     })
//   })
// }

// custtomPromiseAll([p1, p2, p3]).then((res) => console.log({res}));



// sum(1)(1,2,3)()

// function curriedSum(...args) {
//   return function(...nextArgs) {
//     if (nextArgs.length===0) {
//       return args.reduce((a,c) => a+=c, 0)
//     }

//     return curriedSum(...args.concat(...nextArgs))
//   }
// }

// const res = curriedSum(1)(1,2,3)()
// console.log({res})





// Memoization Method

// function memoize(fn) {
//   let cache = {};

//   return function(item) {
//     // Cahced Item
//     if (cache[item]) {
//       return cache[item]
//     }

//     const calculatedResult = fn(item)
//     cache[item] = calculatedResult;

//     console.log({cache})
//     return calculatedResult;
//   }
// }

// function square(item) {
//   console.log("calling square method")
//   return item*item;
// }

// const memoizedFunction = memoize(square);
// console.log({memoizedFunction})

// const res1 = memoizedFunction(2);
// console.log({res1})

// const res2 = memoizedFunction(2);
// console.log({res2})


// Infinite Currying Function
// sum(1,2,3)(2,3)(4)


// function curriedSum(...args) {
//   return function(...nextArgs) {
//     if (nextArgs.length===0) {
//       return args.reduce((acc, cumm) => acc+cumm, 0)
//     }

//     return curriedSum(...args.concat(...nextArgs));
//   }
// }

// const res = curriedSum(1,2,3)(2,3)(4)()
// console.log({res})

// Deep cloning of an object

// const obj = {
//   name: "Ganesh",
//   hobbies: ["badminton", "study", { class: 11 }]
// }

// // We will use recursion
// function deepClone(data) {
//   // Base case
//   if (data === null || typeof data!=='object') {
//     return data;
//   }

//   if (Array.isArray(data)) {
//     return data.map(deepClone);
//   }


//   let res = {};

//   for(let key of Object.keys(data)) {
//     res[key] = deepClone(data[key]);
//   }

//   return res;
// }

// const result = deepClone(obj);
// obj.hobbies[2].class=12
// console.log({result})
// console.log({obj})

// let result = new Array(promisesLength)
// console.log()

// // Printing from 1 to 5, after the subsequent delay
// async function print() {
//   for(let i=1; i<=5; i++) {
//     await new Promise((res, rej) => setTimeout(res, i*1000))
//     console.log({i})
//   }
// }


// print();

// function x() {
//   setTimeout(() => {
//     console.log({j})
//   }, 2000)
//   console.log("Namaste JS")
//   let j = 100;
// }

// x()


// function x() {

//   function y() {
//     console.log({a});
//   }
//   let a = 100;

//   return y;
// }

// const res = x()
// console.log({res})
// res()

//Batching of promises, (given an array of promises, resolve them in batches of
// k and return the results, create a fake api call function to simulate resolution)


// const p1  = Promise.resolve(1);
// const p2  = new Promise((res) => setTimeout(()=> res("45"), 4000))
// const p3  = Promise.resolve(3);
// const p4  = Promise.resolve(4);
// const p5  = Promise.resolve(5);
// const p6  = Promise.reject("p6 failed");
// const p7  = Promise.resolve(7);
// const p8  = Promise.reject("p8 failed");
// const p9  = Promise.resolve(9);
// const p10 = Promise.resolve(10);

// const promises = [p1, p2, p3, p4, p5, p6, p7, p8, p9, p10];
  

// async function resolveInBatches(iterablePromises, k) { // where k is the number of promises in batch
//   let result = [];


//   for(let i=0; i<iterablePromises.length; i+=k) {
//     const promiseBatch = iterablePromises.slice(i,i+k);
//     const b = await Promise.allSettled(promiseBatch)
//     console.log({b})
//     result.push(...b);
//   }

//   return result;
// }


// const res = resolveInBatches(promises, 2)
// console.log({res})












// Flattening of an object

// const obj = {
//   name: "Ganesh Kumar",
//   class: {
//     ArmySchool: "10",
//     DDPS: "10"
//   },
//   hobbies: {
//     sport: "badminton",
//     reading: "halfGF"
//   }
// }

// function flattenObj(data, path, store={}) {
//   console.log({data})
//   if (data===null || typeof data!=="object") {
//     store[path] = data
//     return store;
//   }

//   for(const item of Object.keys(data)) {
//     const generateSuffix = path ? `${path}.${item}` : `${item}`
//     flattenObj(data[item], generateSuffix, store)
//   }

//   return store;
// }


// const res = flattenObj(obj, "user", {})
// console.log({res})



// Custom Array.map

// Array.prototype.myReduce = function (callback, initialValue) {
//   if (!this.length) {
//     return initialValue
//   }
//   let result = initialValue;

//   for(let i=0; i<this.length; i++) {
//     result=callback(result, this[i])
//   }

//   console.log({result})
//   return result;
// }

// const arr = [1,2,3]

// arr.myReduce((acc, cumm) => {
//   return acc+cumm
// }, 0)



// 6. Two Sum — return indices
// twoSum([2, 7, 11, 15], 9)   // [0, 1]

// function twoSum(arr, ) {

// }

// const res = twoSum([2, 7, 11, 15], 9)
// console.log({res})


// 5. Rotate array by k steps
// rotate([1,2,3,4,5], 2)    [4,5,1,2,3]

// const data = [1,2,3,4,5]

// function rotate(data, k) {
//   if (!data || data.lenth===1) {
//     return data;
//   }
//   let timeToRotate = k % data.length;

//   console.log({timeToRotate})
//   let low = 0;
//   let high = data.length-1

//   function reverse(arr, start, end) {
//     while(start<end) {
//       [arr[start], arr[end]] = [arr[end], arr[start]]
//       start++
//       end--
//     }
//   }

//   reverse(data, low, high);
//   reverse(data, low, timeToRotate-1)
//   reverse(data, timeToRotate, high)
//   return data;

// }


// const res = rotate([1,2,3,4,5,6,7], 3)
// console.log({res});



// 5. Rotate array by k steps
// rotate([1,2,3,4,5], 2)      // [4,5,1,2,3]


// function rotate(data, rotationIndex) {
  // let toRotate = rotationIndex;
  // if (rotationIndex>data.length) {
  //   toRotate =  rotationIndex % data.length
  // }

  // if(toRotate===data.length) {
  //   return data;
  // }

  // while(toRotate>0) {
  //   let poppedElement = data.pop();
  //   console.log({poppedElement})
  //   data.unshift(poppedElement)
  //   toRotate--;
  // }

  // return data
  
// }

// const res = rotate([1,2,3,4,5], 2)
// console.log({res})


// 4. Chunk array into groups
// chunk([1,2,3,4,5], 2)       // [[1,2], [3,4], [5]]


// function chunk(data, toChunk) {
//   let res = [];
//   // let itemPush=0;
//   let temp=[];

//   for(const item of data) {
//     temp.push(item);
//     if (temp.length===toChunk) {
//       res.push(temp);
//       temp=[]
//     }
//   }

//   if (temp.length) {
//     res.push(temp)
//   }


//   return res;
// }

// const res = chunk([1,2,3,4,5], 2)
// console.log({res})


// findMax([3, 1, 4, 1, 5, 9]) // 9
// findMin([3, 1, 4, 1, 5, 9]) // 1


// function findMaxMin(data) {
//   let min=Infinity
//   let max=-Infinity;

//   for(const item of data) {
//     if(item<min) {
//       min=item
//     }
//     if (item>max) {
//       max=item
//     }
//   }

//   return { min,max }
// }

// const res = findMaxMin([3, 1, 4, 10, 5, 9])
// console.log({res})


// 2. Remove duplicates
// unique([1, 2, 2, 3, 3, 3])  // [1, 2, 3]

// function unique(data) {
//   let i=0;
//   for(let j=1; j<data.length; j++) {
//     if (data[j]!==data[j-1]) {
//       data[i+1]=data[j];
//       i++
//     }
//   }

//   return data
// }

// const res = unique([1, 2, 2, 3, 3, 3])
// console.log({res})



// 29. Implement Array.flat with depth
// myFlat([1,[2,[3,[4]]]], 2)  // [1,2,3,[4]]

// function myFlat(data, depth, result=[]) {
//   for(const item of data) {
//     if (Array.isArray(item) && depth>0) {
//       myFlat(item, depth-1, result)
//     } else {
//       result.push(item)
//     }
//   }
//   return result
// }

// const res = myFlat([1,[2,[3,[4]]]], 0)
// console.log({res})

// 28. Flatten using reduce only
// flattenReduce([1,[2,[3,[4]]]])  // [1,2,3,4]

// function flattenReduce(data, result=[]) {
//   for(const item of data) {
//     if(Array.isArray(item)) {
//       flattenReduce(item, result)
//     } else {
//       result.push(item)
//     }
//   }
//   return result;
// }

// const res = flattenReduce([1,[2,[3,[4]]]])
// console.log({res})


// Custom implementation for Promise.allSettled
/**
 * returns us a promise -> [{status: "", value: ""}, {status: "", value: ""}, {status: "", value: ""}]
 */


// function allPromiseSettled(iterablePromises) {
//     return new Promise((res, rej) => {
//         if (!iterablePromises.length) {
//             return rej("No promises sent")
//         }
//         const result = new Array(iterablePromises.length);
//         console.log({result})
//         let resolved = 0;

//         iterablePromises.forEach((it, index) => {
//             Promise.resolve(it).then((val) => {
//                 result[index] = {
//                     status: "fulfilled",
//                     value: val
//                 }
//             }).catch((err) => {
//                 result[index] = {
//                     status: "rejected",
//                     reason: err
//                 }
//             }).finally(() => {
//                 resolved++;
//                 if (resolved===iterablePromises.length) {
//                     res(result)
//                 }
//             }) 
//         })
//     })
// }

// const p1 = 42;
// const p2 = Promise.resolve(34);
// const p3 = Promise.reject("police verification")
// const res = allPromiseSettled([p1, p2, p3])
// console.log({res})




// async function getData() {
//     console.log("1")
//     await new Promise((res, rej) => res("Promise Resolved"))
//     console.log("2")
// }

//  getData()
// console.log("Hello")


// Infinite Currying with n number of argyments

/***
 * Sample Input
 * -> currySum(1)(1,2,3)(23)()
 */

// function sum(...args) {
//   return (...nextArgs) => {
//     if (!nextArgs.length) {
//       return args.reduce((acc, cumm) => {
//         return acc+=cumm
//       }, 0 )
//     }
//     return sum(...args.concat(...nextArgs))
//   }
// }

// const res = sum(1)(1,2,3)(23)()
// console.log({res})

// console.log({a})

// function a() {
//     console.log("Hello world")
// }
// var a = 5;


// Polyfill of Apply in js
// Function.apply(this, [arg1, arg2, arg3])


// Function.prototype.customApply = function(this) {
//     console.log(this)
// }


// function MyInfo(name) {
//     console.log("My Name is >>", {name})
// }

// const res = MyInfo.customApply(this)
// console.log({res});



// Square Root of a number

// let num = 26;


// function findSqrt(num) {

    
//     if (num<2) {
//         return num;
//     }
    
//     let low = 1;
//     let high = Math.floor(num/2);
    
//     while(low<=high) {
//         let mid = Math.floor((low+high)/2);
        
//         let multiplyByTwo = mid*mid;
        
//         if (multiplyByTwo===num) {
//             return mid;
//         }
        
//         if (multiplyByTwo>num) {
//             high = mid-1;
//         } else {
//             low = mid+1
//         }
//     }
    
//     return low;
    
// }

// const res = findSqrt(2)
// console.log({res})

// /**
//  * @param {number[]} nums1
//  * @param {number[]} nums2
//  * @return {number[]}
//  */
// var nextGreaterElement = function(nums1, nums2) {
//     let bucket = [];
//     let nextGreaterMap = {};

//     for(const item of nums2) {

//         if (bucket.length>0 && item>bucket[bucket.length-1]) {
//             const prev = bucket.pop();
//             nextGreaterMap[prev] = item;
//         }
//         bucket.push(item)
//     }

//     while(bucket.length>0) {
//         nextGreaterMap[bucket.pop()] = -1;
//     }


//     console.log({nextGreaterMap})

//     return nums1.map((item) => nextGreaterMap[item]);
// };


// TWO SUM PROBLEM

// const nums = [2, 7, 11, 15];
// const target = 9;

// function twoSum(nums, target) {
//   const hash = {};

//   for(let i=0; i< nums.length; i++) {
//     const requiredAnotherNumber = target - nums[i];
//     if (hash.hasOwnProperty(requiredAnotherNumber)) {
//       return [hash[requiredAnotherNumber], i];
//     } else {
//       hash[nums[i]] = i
//     }
//   }
//   console.log({hash})

// }

// const res= twoSum(nums, target)
// console.log({res})


// const products = [
//   { id: 1, name: 'Laptop', category: 'Electronics', price: 999 },
//   { id: 2, name: 'Shirt', category: 'Clothing', price: 29 },
//   { id: 3, name: 'Phone', category: 'Electronics', price: 699 },
//   { id: 4, name: 'Pants', category: 'Clothing', price: 49 },
//   { id: 5, name: 'Tablet', category: 'Electronics', price: 399 }
// ];


// const resObj = {};

// for(const item of products) {
//   if(resObj[item.category]) {
//     resObj[item.category].push(item)
//   } else {
//     resObj[`${item.category}`] = [item]
//   }
// }

// console.log({resObj})

// 'use strict'

// let obj = {
//   x: 10,

// }


// Custom Promise.race()


// const p1 = Promise.resolve(45);
// const p2 = Promise.reject(12);


// function customPromiseRace(items) {
//   return new Promise((res, rej) => {
    
//     items.forEach((it) => {
//       Promise.resolve(it).then((val) => {
//         res(val)
//       }).catch((data) => {
//         rej(data)
//       }) 
//     })
//   })
// }

// const res = customPromiseRace([p1, p2])
// console.log({res})


// const res1 = customPromiseRace([p1, p2])
// console.log({res1})


// const str = "hello world !!!";

// // Strings are immutable in js
// let result = "";

// let flag = false;

// for(let i=str.length; i>=0; i--) {
//   result+=str.charAt(i)
// }

// console.log({result})

// 

// const arr = [10, 2, 3,30, 40];

// function findSecondLargest(data) {
// 	if (!data || !data?.length) {
// 		return;
// 	}

// 	let firstLargest = -Infinity;
// 	let secondLargest = -Infinity;

// 	for(const item of data) {
// 		if (item>firstLargest) {
// 			secondLargest = firstLargest
// 			firstLargest = item;
// 		} else if (item>secondLargest) {
// 			secondLargest=item
// 		}
// 	}

// 	return secondLargest;
// }

// const res = findSecondLargest(arr);
// console.log({res})


// Promise all Settled

// const p1 = Promise.resolve(45);
// const p2 = 32;
// const p3 = Promise.reject(12);

// function customPromiseAllSettled(...items) {
//     return new Promise((res, rej) => {
//         let resolved = 0;
//         let result = new Array(items.length)

// 				items.forEach((iterablePromise, index) => {
// 					Promise.resolve(iterablePromise).then((it) => {
// 						result[index] = {
// 							status: "fulfilled",
// 							value: it
// 						};
// 						resolved++;
// 					}).catch((it) => {
// 						result[index] = {
// 							status: "rejected",
// 							value: it
// 						}
// 						resolved++;
// 					}).finally(() => {
// 						if (resolved===items.length) {
// 							res(result)
// 						}
// 					})
// 				})
//     })
// }


// const res = customPromiseAllSettled(p1, p2, p3).then((val) => {
// 	console.log({val})
// })
// console.log({res})



// const a = function xyz() {
//     console.log("Calling XYZ")
// }

// const b = function xyz() {
//     console.log("Calling XYZ")
// }

// console.log(a===b)



// Length of last Word

// var lengthOfLastWord = function (s) {
//     if (!s) {
//         return 0;
//     }
//     let lastWord = "";

//     for (let i =0; i<=s.length-1; i++) {
//         if (s.charAt(i)===' ') {
//             lastWord=""
//         } else {
//             lastWord+=s[i]
//         }
//     }

//     return lastWord;    
// };

// const res = lengthOfLastWord("Hello World")
// console.log({res})


// Infinite Currying

// function curriedSum(...args) {
//   let sum = 0;

//   args.forEach((pol) => {
//     sum+=pol
//   })

//   return function nextSum(...next) {
//     if (next.length===0) {
//       return sum;
//     }

//     for(const item of next) {
//       sum+=item;
//     }

//     return nextSum;
//   }
// }

// const res = curriedSum(1,2,3)(4,5)(6)();
// console.log({res})


// BROKEN - fix it!
// function delayedLog(n) {
//   return new Promise(resolve => {
//     setTimeout(() => {
//       console.log(n);
//       resolve(n);
//     }, 100);
//   });
// }

// delayedLog(1)
//   .then(() => delayedLog(2))
//   .then(() => delayedLog(3))



// Flatten Deep Array
// const data = [1, [2, [3, [4]]], 5];
// function flattenDeep(items, res = []) {
//   if (!items) {
//     return res;
//   }

//   for(const item of items) {
//     if (!Array.isArray(item)) {
//       res.push(item)
//     } else {
//       flattenDeep(item, res)
//     }
//   }
//   return res
// }

// const res = flattenDeep(data);

// console.log({res})

// Memoization using closures

// function memoizemultiply(factor) {
//   let cached = {}
//   let fac = factor


//   return function (num) {
//     if (cached[num]) {
//       return cached[num]
//     }

//     let result = num*fac;
//     cached[num] = result;
//     return result;
//   }
// }

// const memo = memoizemultiply(5)
// console.log("Mem 1 >>", memo(2))
// console.log("Mem 2 >>", memo(3))
// console.log("Mem 3 >>", memo(4))

// Currying

// function curriedSum(...args) {
//   return function(...nextArgs) {
//     if (nextArgs.length>=args.length) {
//       return args.reduce((acc, cum) => acc+=cum, 0)
//     }
//     return curriedSum(...args.concat(...nextArgs))
//   }
// }
// let sum = item;

// function inner(nextArg) {
//   if (!nextArg) {
//     return sum;
//   } else {
//     sum+=nextArg
//     return inner;
//   }
// }
// return inner

// const res = curriedSum(5,1,2)(5,4)()
// console.log({res})


// Deep cloning of an Object

// const obj = {
//   name: "Ganesh",
//   hobbies: {
//     sports: ['badminton', 'athletics']
//   },
//   getName: () => {
//     console.log("Get name is called")
//   },
//   start: new Date()
// }

// function deepClone(data, clonedData = {}) {
//   if (typeof data!==null || typeof data!=='object') {
//     return data;
//   }

//   if (Array.isArray(data)) {
//     return data.map((item) => deepClone(item, clonedData))
//   }

//   for(const [startIndex, item] of Object.entries(data)) {
//     clonedData[startIndex] = deepClone(data[startIndex], clonedData)
//   }

//   return clonedData
// }

// const res = deepClone(obj, {});
// console.log({res})


// const p1 = Promise.resolve(1);
// const p2 = Promise.reject("error")
// const p3 = Promise.resolve(3)

// function promiseAllSettled(promData) {
//   return new Promise((resolve, reject) => {
//     let results = new Array(promData.length);
//     let unresolved = promData.length;

//     if (unresolved===0) {
//       resolve(results);
//     }

//     promData.forEach((item, index) => {
//       Promise.resolve(item).then((data) => {
//         results[index] = {
//           status: "fulfilled",
//           value: data
//         };
//         unresolved--;
//       }).catch((err) => {
//         results[index] = {
//           status: 'rejected',
//           reason: err
//         }
//         unresolved--;
//       }).finally(() => {
//         if (unresolved===0) {
//           resolve(results)
//         }
//       })
//     })
//   })
// }


// const res = promiseAllSettled([p1,p2,p3])
// console.log({res})





// function mainFunction(param) {
//   console.log("Main Function Running !!", {param});
// }


// const debouncerFunc = (fn, time) => {
//   let timerRef = null;

//   return function(...newArgs) {
//     clearTimeout(timerRef)
//     timerRef = setTimeout(() => {
//       fn(...newArgs)
//     }, time)
//   }
// }



// const debounce = debouncerFunc(mainFunction, 2000)


// debounce()
// debounce()
// debounce()
// debounce()

// setTimeout(() => {
//   debounce()
// }, 3000)


// const p1 = new Promise((res, rej) => {
//   setTimeout(()=> {
//     res("Hello")
//   }, 2000)
// })


// async function mockAPICall() {
//   const res = await p1;
//   console.log({res})
// }

// mockAPICall();


// Custom Map, Filter, Reduce

// Array.prototype.myMap = function(callback) {
//   let result = []
//   for(let i=0; i<this.length; i++) {
//     result.push(callback(this[i]))
//   }
//   return result;
// }


// let arr = [1,2,3]

// const res = arr.myMap((it) => {
//   return it*it
// })

// console.log({res})




// Call, Apply, Bind
// 'use strict'
// let name = {
//   firstName: 'Ganesh',
//   lastName: 'Kumar'
// }

// function printData(city) {
//   console.log(this)
//   console.log("Name is :",this.firstName+' ',this.lastName, `lives in ${city}`)
// }

// printData.call(name, 'Ghaziabad')



// Promise.all custom implementation

// const p1 = new Promise((res, rej) => rej(45));
// const p2 = new Promise((res, rej) => {
//   setTimeout(() => {
//     rej("Happy")
//   }, 2000)
// })
// // const p3 = 12;

// // console.log("Items >>>", new Array(4))

// function customPromiseAny(allPromises) {
//   return new Promise((res, rej) => {
//     if (!allPromises.length) {
//       res([])
//       return;
//     }
    
//     let unresolved = allPromises.length;
//     let results = new Array(allPromises.length);

//     allPromises.forEach((item, ind) => {
//       Promise.resolve(item).then((data)=> {
//         res(data)
//       }).catch((reason) => {
//         results[ind] = reason;
//         unresolved--;
//         if (unresolved===0) {
//           rej(results);
//         }
//       })
//     })
//   })
// }


// const res = customPromiseAny([p1, p2])
// console.log({res})




// Infinite Currying
// sum(1,2,3)(4,5,6)(7,8)


// function sum(...args) {
//   return (...nextArgs) => {
//     if (!nextArgs.length) {
//       return args.reduce((acc, cumm) => {
//         return acc+=cumm
//       }, 0 )
//     }
//     return sum(...args.concat(...nextArgs))
//   }
// }


// const res = sum(1, 2, 3)(4, 5, 6)(7, 8)()
// console.log({ res })


// Custom LRU Cache

// class LRUCache {
//   constructor(capacity) {
//     this.capacity = capacity;
//     this.cache = new Map();
//   }

//   put(it) {
//     if (this.cache.has(it)) {
//       this.cache.delete(it)
//     }


//     this.cache.set(it, it)

//     if (this.cache.size > this.capacity) {
//       let lruKey = this.cache.keys().next().value;
//       this.cache.delete(lruKey)
//     }
//   }

//   get(id) {
//     const fetchResult = this.cache.has(id)
//     if(!fetchResult) {
//       console.log("No Key Present for the id >>" , id)
//       return;
//     }

//     const getResult = this.cache.get(id)

//     this.cache.delete(id)
//     this.cache.set(id, getResult)

//     return getResult
//   }
// }


// const cache = new LRUCache(5);
// cache.put(1, 1);
// cache.put(2, 2);
// cache.put(3, 3);
// cache.put(4, 4);
// cache.put(5, 5);
// cache.put(6, 6);
// cache.put(7, 7);
// cache.put(8, 8);
// cache.put(9, 9);

// const get4 = cache.get(4)
// console.log("get 4 >>", get4)





// Custom Filter Method

// Array.prototype.myFilter = function(callback) {
//   let result = []


//   for(let i=0;i<this.length; i++) {
//     let temp = callback(this[i])
//     if (temp) {
//       result.push(this[i])
//     }
//   }

//   return result
// }


// const arr = [1,2,3,4,5,6,7,8,9, 10];

// const res = arr.myFilter(function(val) {
//   return val%2===0;
// })

// console.log({res})


// Memoization Method


// function memoize(fn) {
//   let cache = {}

//   return function(args) {
//     let key = JSON.stringify(args)


//     if (cache[key]) {
//       console.log("Giving result from cache")
//       return cache[key]
//     }

//     console.log("Calculating Result...")

//     const result = fn.call(this, args)
//     cache[key] = result
//     return result;
//   }
// }

// function square (a) {
//   return a*a;
// }

// const memoized = memoize(square)

// const res = memoized(5);
// console.log(res)
// const res1 = memoized(5);
// console.log(res1)

// Flattening of a nested Array

// const arr = [1,2,3, [4,5], [6, [7,8, [9,10]]]];


// function nestedArray(data, store) {
//   for(const item of data) {
//     if (!Array.isArray(item)) {
//       store.push(item)
//     } else {
//       nestedArray(item, store)
//     }
//   }

//   return store;
// }

// const res = nestedArray(arr, [])
// console.log({res})


// Deep cloning and Flattening of an object

// const data = {
//   name: "Ganesh",
//   study: {
//     '12': 'Army_School'
//   }
// }


// Flattening of an object

// function flattenObj(data, path, store) {
//   if (typeof data!=='object' || data===null) {
//     store[path] = data;
//     return store;
//   }


//   for(const item in data) {
//     let generateSuffix = path ? `${path}.${item}` : `${item}`;
//     console.log("suffix >>", {generateSuffix})
//     flattenObj(data[item], generateSuffix, store)
//   }

//   return store;

// }


// const res = flattenObj(data, 'user', {})
// console.log({res})



// function deepClone(item) {
//   if (typeof item !== 'object' && item!==null) {
//     return item;
//   }

//   if (Array.isArray(item)) {
//     return item.map(deepClone);
//   }

//   const r = {}

//   for(const keyp in item) {
//     r[keyp] = deepClone(item[keyp])
//   }


//   return r
// }


// const res = deepClone(data)


// console.log({res})



// Polyfill for Promise.race

// const p1 = new Promise((res, rej) => {
//    setTimeout(() => {
//      rej("P1 Finished")
//    }, 2000)
// })

// // const p2 = 45;
// const p3 = Promise.reject(3);

// function promiseAny(promises) {
//   return new Promise((resolve, reject) => {
//     let errors = new Array(promises.length)
//     let counter = 0;
//     promises.forEach((p, index) => {
//       Promise.resolve(p).then((val) => {
//         resolve(val)
//         counter++;
//       }, (reason) => {
//         errors[index] = reason
//         counter++
//       }
//     ).finally(() => {
//       if (counter === promises.length) {
//         reject(errors)
//       }
//     })
//     })
//   })
// }

// const results = promiseAny([p1, p3])
// console.log({results})


// Polyfill for Promise.allSettled

// const p1 = new Promise((res, rej) => {
//   setTimeout(() => {
//     res("P1 Finished")
//   }, 1000)
// })

// const p2 = 45;
// const p3 = Promise.reject(3);

// function promiseAllSettled(iterablePromises) {
//   return new Promise((resolve, reject) => {
//     const results = [];
//     let completed = 0;

//     iterablePromises.forEach((item, index) => {
//       Promise.resolve(item).then((val) => {
//         results.push({
//           status: 'fulfilled',
//           value: val
//         })
//       }).catch((reason) => {
//         results.push({
//           status: 'rejected',
//           value: reason
//         })
//       }).finally(() => {
//         completed++;
//         if (completed===iterablePromises.length) {
//           resolve(results)
//         }
//       })
//     })
//   })
// }

// const res = promiseAllSettled([p1, p3, p2])
// console.log({res});



// Polyfill for Promise.all

// const p1 = new Promise((res, rej) => {
//   setTimeout(() => {
//     res("P1 Finished")
//   }, 1000)
// })

// const p2 = 45;
// const p3 = Promise.reject(3);


// function promiseAll(iterable){
//   return new Promise((resolve, reject) => {
//     let results = new Array(iterable.length);

//     let unresolved = iterable.length;


//     if (unresolved===0) {
//       resolve(results);
//       return;
//     }

//     iterable.forEach((item, index) => {
//       Promise.resolve(item).then((val) => {
//         results[index] = val;
//         unresolved -= 1;


//         if (unresolved===0) {
//           resolve(results);
//           return;
//         }
//       })
//     })
//   })
// }

// const res = promiseAll([p1, p2, p3])
// console.log(res)


// Array.prototype.myMap = function(callback) {
//   console.log("Inside prototype running", this)
//   let result = [];

//   for(let i=0; i<this.length; i++) {
//     const temp = callback(this[i], i, this)
//     if (temp) {
//       result.push(this[i])
//     }
//   }
//   return result;
// }

// const arr = [1,2,3,4, 10]

// const output = arr.myMap(function(val, index, array){
//   console.log("val: ", val, 'index: ', index, 'array: ', array);
//   return val%2===0;  
// })

// console.log({output})




// const app = new Map();

// app.set("Name" , "Ganesh")


// console.log("hasProperty >>", app.has("Name"))


// const temp = new Set()
// temp.add(function abc() {
//   console.log("hello");
  
// })
// temp.add(function abc() {
//   console.log("hello");
  
// })
// temp.add("happyi")



// console.log({temp})





// console.log(a);
// var a = 1;

// function a() {
//   console.log("function");
// }

// console.log(a);



// console.log(foo)

// var foo = function () {
//   console.log("hello");
// };



// Usage of this keyword
// "use strict"

// function show() {
//   console.log(this)
// }

// show()

// Closure Example

// let abc = 1000;

// function x() {

//   function y() {
//     console.log(abc);
//   }

//   return y;
// }

// const result = x();
// console.log(result())

// Custom Promise.all

// const p0 = Promise.resolve(3);
// const p1 = 42;
// const p2 = new Promise((resolve, reject) => {
//   setTimeout(() => {
//     resolve('foo');
//   }, 100);
// });

// function promiseAll(iterable) {
//   return new Promise((resolve, reject) => {
//     const results = new Array(iterable.length);
//     let unresolved = iterable.length;


//     if (unresolved===0) {
//       resolve(results);
//       return;
//     }

//     iterable.forEach((item, index) => {
//       Promise.resolve(item)
//        .then((val) => {
//         results[index] = val;
//         unresolved -= 1;

//         if (unresolved === 0) {
//           resolve(results);
//         }
//       },
//       (reason) => {
//         reject(reason);
//       }
//     )
//     })

//   })
// }

// const res = promiseAll([p0, p1, p2])
// console.log({res})


// Data Sanitisation

// const user = {
//     name: "Ganesh",
//     education: {
//         ArmySchool: "10",
//         Dehradun: "12"
//     },
//     hobbies: {
//         Travel: "1"
//     }
// }


// function sanitiseData(data, path, result) {
//   if (typeof data!=='object' || data===null) {
//     result[path] = data
//     return result;
//   }

//   for(let item in data) {
//     let generateSuffix = path ? `${path}.${item}` : `${item}`;
//     sanitiseData(data[item], generateSuffix, result)
//   }

//   return result

// }

// const res = sanitiseData(user, "user" ,{})
// console.log({res})

// const p1 = Promise.resolve(34)
// console.log({p1});



// Generative Functions


// function* myFunc() {
//   console.log("Hello 1")
//   yield 1;

//   console.log("Hello 2")
//   yield 2;

//   console.log("Hello 3")
//   yield 3;
// }

// const gen = myFunc()




// Method Chaining/ Fluent Interface / Builder Pattern

// function calculate(a) {
//   let data = a
//   const api =  {
//     multiply: (b) => {
//       data = data*b;
//       return api;
//     },
//     sum: (b) => {
//       data = data+b
//       return api;
//     },
//     value: () => {
//       return data;
//     }
//   }

//   return api;
// }

// const res = calculate(5).sum(5).multiply(2).value()
// console.log({res})

// TODO:



// Function Currying in JS

// function sum(a) {
  
//   let sum = a;
  
//   function inner(b) {
//     if (arguments.length===0) {
//       return sum;
//     }
//     sum+=b
//     return inner;
//   }
  
//   return inner
// }

// const res = sum(1)(2)(0)()
// console.log({res})





// Polyfill for bind method

// Function.prototype.mybind = function(context, ...args) {
//   let obj = this;

//   return function() {
//     return obj.call(args[0])
//   }
// }

// Custom Deep clone method

// const obj = {
//   name: "Ganesh",
//   hobby: ['adventure', 'sports'],
//   studies: {
//     class: "12"
//   }
// }


// I will use recursion with base condition

// function deepClone(data) {
//   if (typeof data!=='object' || data===null) {
//     return data;
//   }

//   if(Array.isArray(data)) {
//     return data.map(deepClone)
//   }

//   const clone = {};
//   for(const key in data) {
//     clone[key] = deepClone(data[key])
//   }

//   return clone;
// }

// const res = deepClone(obj)

// obj.name = "Rahul";

// console.log({obj})
// console.log({res})




// await Promise.resolve(5)

// Promise.resolve(5).then(...)

// let p = Promise.resolve()

// for (var i = 1; i <= 5; i++) {
//   // setTimeout(() => console.log(i), 0);
//   // p=p.then(() => {
//     // console.log({i})
//   // })
  
//   (function(j){
//     const p1 = Promise.resolve(j).then(val => console.log(val));
//   })(i)
// }




// console.log("A");

// Promise.resolve()
//   .then(() => console.log("B"))
//   .then(() => console.log("C"));

// console.log("D");

// setTimeout(() => console.log("E"));

// Promise.resolve()
//   .then(() => console.log("F"));

// console.log("G");


// const p1 = new Promise((res, rej) => {
//   setTimeout(() => {
//     res("Hello User !!")
//   }, 1000)
// });

// p1.then((val) => {
//   console.log(val)
// })
// console.log(p1)

// console.log("Hello vidhi")

// const arr = [1, 2, [3, [7, [9, 10], 8], 4], 5];
// const DEFINE_LEVEL = 2;

// function customFlat(data, result, level) {
//   if (!Array.isArray(data)) {
//     result.push(data);
//     return result;
//   }

//   for (let i = 0; i < data.length; i++) {
//     if (Array.isArray(data[i]) && level > 0) {
//       customFlat(data[i], result, level - 1);
//     } else {
//       result.push(data[i]);
//     }
//   }

//   return result;
// }

// const res = customFlat(arr, [], DEFINE_LEVEL);
// console.log({ res });

// const original = {
//   name: "Ganesh",
//   address: {
//     city: "Delhi",
//   },
// };

// const copy = { ...original };

// copy.name = "Kumar"; // OK, this is independent
// copy.address.city = "Mumbai";

// console.log(copy);

// function test(...temp) {
//   console.log(temp);
// }

// test("Ganesh", "rahul");

// const obj = {
//   name: "Ganesh",
//   regularFn: function () {
//     const res = () => {
//       console.log("this: ", this);
//     };
//     res();
//   },
//   arrowFn: () => {
//     console.log("arrow:", this);
//   },
// };

// obj.regularFn();

// const timer = setTimeout(() => {
//   console.log("timer running");
// }, 5000);
// console.log({ timer });

// add(1)(2)(3)

// const calculate = {
//   sum: 0,
//   ten: function (a) {
//     this.sum += a * 10;
//     return calculate;
//   },
//   hundred: function (a) {
//     this.sum += a * 100;
//     return calculate;
//   },
//   thousand: function (a) {
//     this.sum += a * 1000;
//     return calculate;
//   },
// };

// const res = calculate.ten(1).hundred(2).thousand(3).sum;
// console.log(res);

// function add(val) {
//   let sum = 0;

//   sum += val;

//   function inner(i) {
//     if (i === undefined) return sum;
//     sum += i;
//     return inner;
//   }

//   return inner;
// }

// const res = add(2)(3)();
// console.log(res);




// const str = "()[]{}";

// function validParenthesis(data) {
  
//   let stack = [];

//   for(let item of data) {
//     if (!stack?.length) {
//       stack.push(item);
//       continue;
//     }
//     let topEle = stack[stack.length-1];
//     if (topEle==='(' && item===')') {
//       stack.pop()
//     } else if (topEle==='{' && item==='}') {
//       stack.pop()
//     } else if (topEle==='[' && item===']') {
//       stack.pop()
//     } else {
//       stack.push(item)
//     }
//   }

//   return stack.length === 0

// }

// validParenthesis(str)

// const sample = "bbbbbbbbb"; // bbbbbbbb

// function longestNonRepeating(s) {
//   const dataLength = s.length;
//   let max = 0;
//   let left = 0;
//   let right = 0;
//   let seen = {};

//  while (right < dataLength) {
//     const characterItem = s.charAt(right);
//     let calDistance = 0;

//     if (seen[characterItem] !== undefined || seen[characterItem] >= left) {
//       left = seen[characterItem] + 1;
//     }
//     seen[characterItem] = right;
//     calDistance = right - left + 1;
//     max = Math.max(max, calDistance);

//     right++;
//   }

//   return max


// }

// const res = longestNonRepeating(sample);
// console.log({res});



// function recursion(num, target) {
//   if (num > target) {
//     return;
//   }
//   console.log(num);
//   recursion(num+1, target);
// }

// recursion(1, 10);



// const n1 = [2, 7, 10];
// const n2 = [1, 2, 3];




// function mergeSorted(ar1, ar2) {
//     const ar1Copy = ar1.map((el) => el)
//     const arr2 = ar2;

//     let p=0,  q=0;

//     for(let i=0; i<(ar1.length+ar2.length); i++) {
//         if (ar1Copy[p] < arr2[q]) {
//             ar1[i] = ar1Copy[p];
//             p++;
//         } else {
//             ar1[i] = ar2[q];
//             q++
//         }
//     }

//     return ar1;

// }

// const res = mergeSorted(n1, n2);
// console.log({res})
