# How to implement .map with .reduce in Javascript

## Introduction

Array in Javascript comes with many built-in methods that accept callback functions. We can add, remove, replace, delete, and perform various operations with the help of these methods. In this blog, we will look at two widely used array methods -

- .map()
- .reduce()

### 1. map

As the name suggests, it **maps** a function to every element and creates a new array with the results of calling a callback function on each element in the array.

Syntax:

```javascript
const resultArray = array.map(function (currentValue, index, array) {
  // return element to resultArray
});
```

- resultArray - the array that is returned
- currentValue - the current value being processed
- index - the index of the currentValue
- array - the array which is being processed

Let's take a look at this simple example:

```javascript
const evenNumbers = [0, 2, 4];

const oddNumbers = evenNumbers.map(function (el) {
  return el + 1;
});

// The above expression with arrow function syntax
const oddNumbers = evenNumbers.map((el) => el + 1);

console.log(oddNumbers); // [1, 3, 5]
```

Here's a concise explanation of above example:

1. In the first iteration, the index is 0, el is 0.

   > el => el + 1 = 1 &nbsp; // [1]

2. In the second iteration, the index is 1, el is 2.

   > el => el + 1 = 3 &nbsp; // [1, 3]

3. In the third iteration, the index is 2, el is 4.

   > el => el + 1 = 5 &nbsp; // [1, 3, 5]

The same logic without the use of .map() method:

```javascript
const evenNumbers = [0, 2, 4];
const oddNumbers = [];

for (let num of evenNumbers) {
  oddNumbers.push(num + 1);
}
```

As you can see, the **map** is really easy to work with compared to the traditional approach. Array methods are really flexible and give you a lot of power, you can even additionally chain other methods to it.

### 2. reduce

It takes an array and **reduces them down in a single value**.

Syntax:

```javascript
const result = array.reduce((accumulator, currentValue) => {
  // perform some operation
}, startValue);
```

It accepts atleast 2 parameters and 1 optional parameter:

- accumulator - stores the end result of the reduce
- currentValue - the current value being processed
- startValue - optional value, if specified is the start value else accumulator acts as the first value

Let's consider this simple example:

```javascript
let sum = [3, 5, 7, 9, 11].reduce(accumulator, currentValue) => {
  return accumulator + currentValue
}
sum; // 35
```

Let's breakdown the above example:
| Callback    | accumulator | currentValue | return value |
| :---------- | :---------: | :----------: | :----------: |
| first call  |      3      |      5       |      8       |
| second call |      8      |      7       |      15      |
| third call  |     15      |      9       |      24      |
| fourth call |     24      |      11      |      35      |

1. In the first call, the accumulator starts as the first element in the array (3) and currentValue (5) starts as the next element in the array. After addition, the result is 8 which is stored as an accumulator for the next iteration.
2. In the second call, now the accumulator is 8, and currentValue is 7, after the addition result is 15 that is the accumulator for the next iteration.
3. This process is repeated for all the elements of the array when the condition is true and the final accumulated result is returned and stored in the sum variable.

Thus, reduce is really useful when you want to perform some operation on arrays or objects and **reduce** it down into a single result. Other use cases of using reduce - finding max/mix, calculating overall product, etc.

## Conclusion

- In this article, we saw two commonly used array methods - map and reduce.
- The .map() method returns a new array after computing upon the original array. You should use the .map() method, when you want to use the result of the array for further operations.
- The .reduce() loops over an array and **collects the result in a single value**.
- Other methods can be chained with the map and reduce method.
- If the method is not explicitly returned, undefined is returned by default.

If you have any questions or feedback, feel free to reach out to me on [Twitter](https://twitter.com/vinitraut18), [Github](https://github.com/vin18) or [Linkedin](https://www.linkedin.com/in/vinit-raut-404651148/).
