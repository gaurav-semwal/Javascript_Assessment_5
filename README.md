# Question No.1 What is the output of this code snippet? Why?
```js
console.log("start");
const promise1 = new Promise((resolve, reject) => {
  console.log(1);
  resolve(2);
  console.log(3);
});
promise1.then((res) => {
  console.log(res);
});
console.log("end");
```
* Output
```js
start
1
3
end
2
```
`Explanation =>` The first line will simply print "start" to the console. Than we have created a new promise and passed the two arguments
(resolve, reject), this function will be executed whenever the promise is created. On the next line again the 1 will be simply printed as this line logs the number 1 to the console. Now the resolve function is called with value 2 means the promise will be fulfilled with the value 2, this following code will be executed asynchronous after the current synchronous execution of code is finished. Again, the next line will simply print 3 as this line logs the number 3 to the console.
On the next step which is promise.then it will register a function to execute, when the promise will be fulfilled till then it will be in queue as promise is an asynchronous function. On next line it will print "end" to the console. Atlast the "2" will be log after the "end" because the callback will act synchronously when the promise was already resolved.

# Question No.2 What is the output of this code snippet? Why?
```js
console.log("start");
setTimeout(() => {
  console.log("setTimeout");
});
Promise.resolve().then(() => {
  console.log("resolve");
});
console.log("end");
```
* Output
```js
start
end
resolve    
setTimeout
```
`Explanation =>` First "start" is logged to the console and than the "setTimeout and "resolve" will not execute direct bcz they are asynchronous 
operations so it will be be execute later after the synchronous code will finished. Now the "end" will logged to console and now as all the synchronous code has finished executing, the remaining operations will start execute means now it will execute resolve as promise is resolved
synchronously and its callback is executed immediately after the promise is created and lastly the "setTimeout" will execute after all the synchronous code has finished executing

# Question No.3 What is callback hell? Write an example to convert callback hell to promise.
`Explanation =>` `* Calback hell` is a scheme where multiple callbacks are nested together means where a callback is called inside another callback. It is the nesting of multiple callbacks inside a function and if we see it just seem like a pyramid.

`Example`:
```js
function sem() {
return new Promise((resolve) => {
console.log("Appinventiv");
resolve();
});
}

function sem1() {
return new Promise((resolve) => {
setTimeout(() => {
console.log("Appinventiv_1");
resolve();
}, 2000);
});
}

function sem2() {
return new Promise((resolve) => {
setTimeout(() => {
console.log("Appinventiv_2");
resolve();
}, 3000);
});
}

async function output() {
await sem();
await sem1();
await sem2();
}

output();
```
# Question No.4 What is the output of this code snippet? Why?
```js
function createIncrement() { 
  let count = 0; 
  function increment() {
   count++; 
  } 
  let message = `Count is ${count}`; 
 function log() { 
  console.log(message); 
  } 
  return [increment, log]; 
 } 
  const [increment, log] = createIncrement(); 
  increment(); 
 increment(); 
increment(); 
log();
```
* Output :
  ```js
  Count is 0
  ```
  `Explanation =>` We have created a function that defines createIncrement function which is a closure that have two functions i.e increment and log and also both of them have variable which is count and message. Inside the count variable we have declared the value 0. Now we have created variable message and assigned the string "Count is" and include the current value of count. The function log is declared within the createIncrement function and will log the messsage variable to the console. Now the return array from createIncremnet is destructured, and the functon 'increment' and 'log' are assigned to variable. Now we have called increment function three times which will increase the count by 1 but when the log function is called it will print the initial value of message which is 0 becuase message was set only once during the creation of createIncrement functon.

 # Question No.5 Extract the data from the API https://jsonplaceholder.typicode.com/users and print name, email id, phone number and company name from the extracted data.
 `Code` :
 ```js
async function semwal() {
  try {
    const get = await fetch("https://jsonplaceholder.typicode.com/users");
    const data = await get.json();
    data.forEach((element) => {
      console.log(`Name :${element.name}`);
      console.log(`Email Id :${element.email}`);
      console.log(`Phone Number :${element.phone}`);
      console.log(`Company Name :${element.company.name}`);
      console.log("⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯");
    });
  } catch(Error) {
    console.log("ERROR OCCURED");
  }
}
semwal();
```
 # Question No.6 Explain and write a code snippet for the following:-
# a).  Promise.all()
# b). Promise.allSettled()
# c). Promise.any()
# d). promise.race()
`Explanation` :
* a). Promise.all() => The Promise.all() is the method which returns a single Promise that resolves means it will provide an array containing the resolved values of all the input promises. But if any of the promise is rejected than all the new promise returned by promise.all will be rejected.
```js
let a = Promise.resolve(7642);
let b = new Promise(function(resolve, reject) {
resolve([ 5000, "APPINVENTIV"]);
});
Promise.all([a, b]).then((resolve)=>{
console.log(resolve)}).catch((error) => {
console.log("ERROR OCCURED")})
```
* b). Promise.allSettled() => The Promise.allSettled is the method which returns a new promise that resolves when all the input are settled i.e either fulfilled or rejected.
```js
const a = Promise.resolve(9090);
const b = new Promise(function (resolve, reject) {
  reject("ERROR DETECT"), resolve();
});
const promises = [a, b];

Promise.allSettled(promises).then((resolve) => console.log(resolve))
.catch((error) => console.log("ERROR DETECT"));
```
* c). Promise.any() => It is a method that helps us to handle multiple promises but only cares about the first promise which resolve. If at least one promise resolves, it gives us the result of that promise, and if all promises are rejected, it gives us an error from the first rejected promise.
```js
const a = new Promise((resolve,reject) => {
resolve("SUCCEED")
});
const b = new Promise((resolve, reject) => {
reject("REJECTED");
});
Promise.any([a,b]).then((resolve) => {
console.log(resolve);
}).catch((reject) => {
console.log(reject);});
```
* d). Promise.race() => This method takes an array of promises as input and returns a new promise. It waits for the first promise in the array to either resolve or reject and then provides the result of that settled promise. It does not wait for other promises either if they are pending or settled, only the result of the first outcome is matters.
```js
const a = new Promise((reject) => {
reject("FAILED");
});
const b = new Promise((resolve) => {
resolve("PASSED");
});
Promise.race([a, b]).then((resolve) => {
console.log(resolve);
}).catch((reject) => {
console.log(reject);
});
```











