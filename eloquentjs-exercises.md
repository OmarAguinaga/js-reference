## FizzBuzz

Write a program that uses console.log to print all the numbers from 1 to 100, with two exceptions. For numbers divisible by 3, print "Fizz" instead of the number, and for numbers divisible by 5 (and not 3), print "Buzz" instead.

When you have that working, modify your program to print "FizzBuzz", for numbers that are divisible by both 3 and 5 (and still print "Fizz" or "Buzz" for numbers divisible by only one of those).

````js
function FizzBuzz() {
  for (var i = 1; i <= 100; i++) {
    var result = '';
    if(i % 3 === 0){
      result += 'Frizz';
    }else if (i % 5 === 0) {
      result += 'Buzz';
    }
    console.log(result || i);
  }
}
FizzBuzz(100)
````

## Chess board

Write a program that creates a string that represents an 8×8 grid, using newline characters to separate lines. At each position of the grid there is either a space or a “#” character. The characters should form a chess board.

````js
function chessBoard() {
  var size = 8;
  var board = '';

  for (var i = 0; i < size; i++) {
    for (var j = 0; j < size; j++) {
      if((i+j) % 2 === 0) {
        board += ' ';
      }else {
        board += '#';
      }
    }
    board += '\n';
  }
  console.log(board);
}
chessBoard();
````

## Recursion

We’ve seen that % (the remainder operator) can be used to test whether a number is even or odd by using % 2 to check whether it’s divisible by two. Here’s another way to define whether a positive whole number is even or odd:

 Zero is even.

 One is odd.

 For any other number N, its evenness is the same as N - 2.

Define a recursive function isEven corresponding to this description. The function should accept a number parameter and return a Boolean.

````js
function isEven(n) {
  if(n == 0) {
    return true
  }else if (n == 1) {
    return false
  }else if(n < 0){
    return isEven(-n-2);
  }else {
    return isEven(n-2);
  }
}

isEven(-50)
````


##The sum of a range

The introduction of this book alluded to the following as a nice way to compute the sum of a range of numbers:

console.log(sum(range(1, 10)));
Write a range function that takes two arguments, start and end, and returns an array containing all the numbers from start up to (and including) end.

Next, write a sum function that takes an array of numbers and returns the sum of these numbers. Run the previous program and see whether it does indeed return 55.

As a bonus assignment, modify your range function to take an optional third argument that indicates the “step” value used to build up the array. If no step is given, the array elements go up by increments of one, corresponding to the old behavior. The function call range(1, 10, 2) should return [1, 3, 5, 7, 9]. Make sure it also works with negative step values so that range(5, 2, -1) produces [5, 4, 3, 2].

````js
function range(start, end, steep) {
  var numbers = [];
  var s = steep || 1;
  for(var i = start; i <= end; i+=s) {
    numbers.push(i);
  }
  return numbers;
}


function sum(numbers) {
  result = 0;
  for(var i = 0; i < numbers.length; i++) {
    result += numbers[i];
  }
  return result;
}



sum(range(1,10,2));
````

## Reversing an array

Arrays have a method reverse, which changes the array by inverting the order in which its elements appear. For this exercise, write two functions, reverseArray and reverseArrayInPlace. The first, reverseArray, takes an array as argument and produces a new array that has the same elements in the inverse order. The second, reverseArrayInPlace, does what the reverse method does: it modifies the array given as argument in order to reverse its elements. Neither may use the standard reverse method.

Thinking back to the notes about side effects and pure functions in the previous chapter, which variant do you expect to be useful in more situations? Which one is more efficient?

````js
function reverseArray(array) {
  var output = [];
  for (var i = array.length - 1; i >= 0; i--)
    output.push(array[i]);
  return output;
}

function reverseArrayInPlace(array) {
  for (var i = 0; i < Math.floor(array.length / 2); i++) {
    var old = array[i];
    array[i] = array[array.length - 1 - i];
    array[array.length - 1 - i] = old;
  }
  return array;
}

console.log(reverseArray(["A", "B", "C"]));
// → ["C", "B", "A"];
var arrayValue = [1, 2, 3, 4, 5];
reverseArrayInPlace(arrayValue);
console.log(arrayValue);
// → [5, 4, 3, 2, 1]
````

## A list

Objects, as generic blobs of values, can be used to build all sorts of data structures. A common data structure is the list (not to be confused with the array). A list is a nested set of objects, with the first object holding a reference to the second, the second to the third, and so on.

````js
var list = {
  value: 1,
  rest: {
    value: 2,
    rest: {
      value: 3,
      rest: null
    }
  }
};
````
The resulting objects form a chain, like this:

A linked list
A nice thing about lists is that they can share parts of their structure. For example, if I create two new values {value: 0, rest: list} and {value: -1, rest: list} (with list referring to the variable defined earlier), they are both independent lists, but they share the structure that makes up their last three elements. In addition, the original list is also still a valid three-element list.

Write a function arrayToList that builds up a data structure like the previous one when given [1, 2, 3] as argument, and write a listToArray function that produces an array from a list. Also write the helper functions prepend, which takes an element and a list and creates a new list that adds the element to the front of the input list, and nth, which takes a list and a number and returns the element at the given position in the list, or undefined when there is no such element.

If you haven’t already, also write a recursive version of nth.

````js
function arrayToList(array) {
  list = null;

  for(var i = array.length - 1; i >= 0; i--){
    list = {value: array[i], rest: list}
  }
  return list
}

function listToArray(list) {
  var array = [];
  for(var node = list; node; node = node.rest){
    array.push(node.value);
  }
  return array;
}

function prepend(value, rest) {
  return {value: value, rest: rest}
}

function nth(list, n) {
  if(!list) {
    return undefined;
  }else if(n == 0) {
    return list.value;
  }else {
    return nth(list.rest, n-1);
  }
}



console.log(arrayToList([10, 20]));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(listToArray(arrayToList([10, 20, 30])));
// → [10, 20, 30]
console.log(prepend(10, prepend(20, null)));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(nth(arrayToList([10, 20, 30]), 1));
// → 20
````


## Deep comparison

The == operator compares objects by identity. But sometimes, you would prefer to compare the values of their actual properties.

Write a function, deepEqual, that takes two values and returns true only if they are the same value or are objects with the same properties whose values are also equal when compared with a recursive call to deepEqual.

To find out whether to compare two things by identity (use the === operator for that) or by looking at their properties, you can use the typeof operator. If it produces "object" for both values, you should do a deep comparison. But you have to take one silly exception into account: by a historical accident, typeof null also produces "object".


````js
function deepEqual(a, b) {
  // Se if they are the same
  if (a === b) return true;

  // se if they are abject or null ad return false it hey are not
  if (a === null || typeof(a) != "object" || b === null || typeof(b) != "object") {
    return false;
  }

  var propsInA = 0, propsInB = 0;
  for (var prop in a) {
    propsInA++;
  }

  for (var prop in b) {
    propsInB++;

    // se if a property in the b bject is in the a object and compare to see if they are equal
    if(!(prop in a) || !deepEqual(a[prop], b[prop])) {
      return false
    }
  }

  return propsInA == propsInB;
}

var obj = {here: {is: "an"}, object: 2};
console.log(deepEqual(obj, obj));
// → true
console.log(deepEqual(obj, {here: 1, object: 2}));
// → false
console.log(deepEqual(obj, {here: {is: "an"}, object: 2}));
// → true
````
