# promise-sequential-throttle
Execute promise in sequence, with throttle.

## Installation

```
npm install --save promise-sequential-throttle
```

sequential.all(sequence, promiseFunction[, throttle]);

 *  sequence: &emsp;  `<array>` | `<generator>`  
    &emsp;&emsp;type: array  
    &emsp;&emsp;&emsp;&emsp;array of parameters that pass in to promiseFunction  
    &emsp;&emsp;type: generator function  
    &emsp;&emsp;&emsp;&emsp;a function that returns a generater object, which generates parameters that pass in to promiseFunction  
    &emsp;&emsp;type: generator object  
    &emsp;&emsp;&emsp;&emsp;a generater object, which generates parameters that pass in to promiseFunction  
 
 * promiseFunction: &emsp;`<function>`  
    &emsp;&emsp;type: function  
    &emsp;&emsp;&emsp;&emsp;task execution function, pass in a parameter, returns a promise  

 
 * throttle: &emsp;`<number>`  
    &emsp;&emsp;type: number  
    &emsp;&emsp;&emsp;&emsp;throttle limit of concurrent executions  

## Usage

Parameter Array

```js
const sequential = require('promise-sequential-throttle');
const params = [1, 2, 3, 4, 5];

sequential.all(params,
	param => new Promise(resolve =>
		setTimeout(() => {
			console.log(param);
			resolve();
		}, 1000)
	)
	, 2)
	.then(() => console.log('All promise finished in sequence'));
```

Generator Function

```js
const sequential = require('promise-sequential-throttle');
const limit = 1000000000000000000000000000000000000000000000;
let i = 0;
const generatorFunction = function* () {
    while (i < limit)
        yield i++;
};

sequential.all(generatorFunction,
	param => new Promise(resolve =>
		setTimeout(() => {
			console.log(param);
			resolve();
		}, 1000)
	)
	, 2)
	.then(() => console.log('All promise finished in sequence'));
```

Generator Object
```js
const sequential = require('promise-sequential-throttle');
const limit = 1000000000000000000000000000000000000000000000;
let i = 0;
const generatorFunction = function* () {
    while (i < limit)
        yield i++;
};
const generatorObject = generatorFunction(); 

sequential.all(generatorObject,
	param => new Promise(resolve =>
		setTimeout(() => {
			console.log(param);
			resolve();
		}, 1000)
	)
	, 2)
	.then(() => console.log('All promise finished in sequence'));
```