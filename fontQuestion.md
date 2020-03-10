<div align="center">
  <h1>20 required JavaScript interview questions</h1>

  ---
  Feel free to reach out to me! 😊 
  </div>

---

###### 1. The difference between undefined and not defined in JavaScript

<details><summary><b>Answer</b></summary>
<p>

If JavaScript does not declare variables to be used directly, an exception will be thrown: `var name is not defined`. If the exception is not handled, the code will stop running. However, the use of `typeof undeclared_variable` does not cause an exception, and it will directly return undefined.
```javascript
var x; // 声明 x
console.log(x); //output: undefined

console.log(typeof y); //output: undefined

console.log(z);  // 抛出异常: ReferenceError: z is not defined
```

</p>
</details>

---

###### 2. What's the output?

```javascript
var y = 1;
if (function f(){}) {
    y += typeof f;
}
console.log(y);
```


<details><summary><b>Answer</b></summary>
<p>

#### Answer: `1undefined`

In JavaScript, if statement evaluation actually uses Eval function, and `eval (function f() {})` returns `function f() {}` which is true.
Now we can transform the code into its equivalent code.

```javascript
var k = 1;
if (1) {
    eval(function foo(){});
    k += typeof foo;
}
console.log(k);
```

The above code output is actually `1 undefined`. Why that? Let's look at the `eval ()` documentation to get the answer

- This method only accepts the original string as a parameter. If the string parameter is not the original string, the method will return without any change.

The return value of `function f() {}` statement is `undefined`, so everything makes sense.
Note that the code above is different from the code below.

```javascript
var k = 1;
if (1) {
    function foo(){};
    k += typeof foo;
}
console.log(k); // output 1function
```


</p>
</details>

---

###### 3. What are the disadvantages of creating a real private method in JavaScript?

<details><summary><b>Answer</b></summary>
<p>

Every object will create a method of private method, which is very memory consuming
Look at the following code

```javascript
var Employee = function (name, company, salary) {
    this.name = name || "";
    this.company = company || "";
    this.salary = salary || 5000;

    // Private method
    var increaseSalary = function () {
        this.salary = this.salary + 1000;
    };

    // Public method
    this.dispalyIncreasedSalary = function() {
        increaseSlary();
        console.log(this.salary);
    };
};

// Create Employee class object
var emp1 = new Employee("John","Pluto",3000);
// Create Employee class object
var emp2 = new Employee("Merry","Pluto",2000);
// Create Employee class object
var emp3 = new Employee("Ren","Pluto",2500);
```

Here, emp1, emp2, and emp3 all have a copy of the increasesalary private method.
So we do not recommend using private methods unless necessary.

</p>
</details>

---

###### 4. What is closure in JavaScript? Write an example

<details><summary><b>Answer</b></summary>
<p>

As the old saying goes, a closure is a function in which another function is declared, and this function accesses variables in the scope of the parent function.
Here is an example of a closure that accesses variables in three domains
- Variables in its own scope
- Variables in the scope of the parent function
- Global scope variables
```javascript
var globalVar = "abc";

// Parent self invoking function
(function outerFunction (outerArg) { // begin of scope outerFunction
    // Variable declared in outerFunction function scope
    var outerFuncVar = 'x';
    // Closure self-invoking function
    (function innerFunction (innerArg) { // begin of scope innerFunction
        // variable declared in innerFunction function scope
        var innerFuncVar = "y";
        console.log(
            "outerArg = " + outerArg + "\n" +
            "outerFuncVar = " + outerFuncVar + "\n" +
            "innerArg = " + innerArg + "\n" +
            "innerFuncVar = " + innerFuncVar + "\n" +
            "globalVar = " + globalVar);
 
    }// end of scope innerFunction)(5); // Pass 5 as parameter
}// end of scope outerFunction )(7); // Pass 7 as parameter
innerFunction is closure that is defined inside outerFunc
```

Output is simple：

```javascript
outerArg = 7
outerFuncVar = x
innerArg = 5
innerFuncVar = y
globalVar = abc
```


</p>
</details>

---

###### 5. Write a mul function as follows

```javascript
console.log(mul(2)(3)(4)); // output : 24
console.log(mul(4)(3)(4)); // output : 48
```

<details><summary><b>Answer</b></summary>
<p>
```javascript
function mul (x) {
    return function (y) { // anonymous function
        return function (z) { // anonymous function
            return x * y * z;
        };
    };
}
```
Simple description: mul returns an anonymous function, and runs the anonymous function to return an anonymous function. The inner anonymous function can access x, y, Z and then calculate the product return.
For functions in JavaScript, the following knowledge points can be inspected:

- Functions are first class citizens
- A function can have properties and can be connected to its constructor
- Functions can exist in memory as a variable
- Functions can be passed as arguments to other functions
- Function can return other functions
</p>
</details>

---


###### 6. How does JavaScript empty arrays?

```javascript
var arrayList =  ['a','b','c','d','e','f'];
```

<details><summary><b>Answer</b></summary>
<p>

##### Method 1
`arrayList = [];`
Directly change the object that ArrayList points to, and the original object does not change.

##### Method 2
`arrayList.length = 0;`
This method clears the elements of the original array by setting length = 0.

##### Method 3
`arrayList.splice(0, arrayList.length);`
Similar to method 2

</p>
</details>

---

###### 7. How to judge whether an object is an array?

<details><summary><b>Answer</b></summary>
<p>

##### Method 1
Use `Object.prototype.toString` to determine whether it is an array

```javascript
function isArray(obj){
    return Object.prototype.toString.call( obj ) === '[object Array]';
}
```
Here we use `call` to point `this` in `toString` to `obj`. Then complete the judgment

##### Method 2
Use prototype chain to complete judgment

```javascript
function isArray(obj){
    return obj.__proto__ === Array.prototype;
}
```
The basic idea is that if an instance is constructed by a constructor, its ` __proto__` is  pointing to the prototype property of constructor.

##### Method 3
Using JQuery

```javascript
function isArray(obj){
    return $.isArray(obj)
}
```
The implementation of jQuery isarray is actually method 1

</p>
</details>

---

###### 8. What's the output?

```javascript
var output = (function(x){
    delete x;
    return x;
})(0);
  
console.log(output);
```

<details><summary><b>Answer</b></summary>
<p>

#### Answer: 0
The delete operator is the operation to delete the attribute of an object. But x here is not an object property, and the delete operator does not work.

</p>
</details>

---

###### 9. What's the output?

```javascript
var x = 1;
var output = (function(){
    delete x;
    return x;
})();

console.log(output);
```

<details><summary><b>Answer</b></summary>
<p>

#### Answer: 1

The delete operator is the operation to delete the attribute of an object. But x here is not an object property, and the delete operator does not work.

</p>
</details>

---

###### 10. What happens when we do this?

```javascript
var x = { foo : 1};
var output = (function(){
    delete x.foo;
    return x.foo;
})();

console.log(output);
```

<details><summary><b>Answer</b></summary>
<p>

#### Answer: undefined

Although x is a global variable, it is an object. Delete works on x.foo and successfully deletes x.foo. So return undefined

</p>
</details>

---

###### 11. What's the output?

```javascript
var Employee = {
    company: 'xyz'
}
var emp1 = Object.create(Employee);
delete emp1.company
console.log(emp1.company);
```

<details><summary><b>Answer</b></summary>
<p>

#### Answer: xyz

Emp1 here inherits the company of employee through prototype. Emp1 has no company attribute of its own. So the delete operator has no effect.

</p>
</details>

---

###### 12. 什么是 undefined x 1 ？

<details><summary><b>Answer</b></summary>
<p>

You can see the figure of undefined x 1 by executing the following code in chrome.

```javascript
var trees = ["redwood","bay","cedar","oak","maple"];
delete trees[3];
console.log(trees);
```
当我们使用 delete 操作符删除一个数组中的元素，这个元素的位置就会变成一个占位符。打印出来就是undefined x 1。注意如果我们使用trees[3] === 'undefined × 1'返回的是 false。因为它仅仅是一种打印表示，并不是值变为undefined x 1。

When we use the `delete` operator to delete an element in an array, the position of the element becomes a placeholder. Printed out is `undefined x 1`. Note that if we use `trees [3] = = 'undefined × 1'`, we return `false`. Because it's just a printed representation, it's not a value that changes to` undefined x 1`.

</p>
</details>

---

###### 13. What's the output?

```javascript
var trees = ["xyz","xxxx","test","ryan","apple"];
delete trees[3];
  
console.log(trees.length);
```

<details><summary><b>Answer</b></summary>
<p>

#### Answer: 5

Because the delete operator does not affect the length of the array.

</p>
</details>

---

###### 14. what's the output?

```javascript
var bar = true;
console.log(bar + 0);
console.log(bar + "xyz");
console.log(bar + true);
console.log(bar + false);
```

<details><summary><b>Answer</b></summary>
<p>
```javascript
1
truexyz
2
1
```
Here is an addition operation table

```javascript
Number + Number -> 加法

Boolean + Number -> 加法

Boolean + Boolean -> 加法

Number + String -> 连接

String + Boolean -> 连接

String + String -> 连接
```

</p>
</details>

---

###### 15. What's the output?

```javascript
var z = 1, y = z = typeof y;
console.log(y);
```

<details><summary><b>Answer</b></summary>
<p>

#### Answer: undefined
The combination law of assignment operation in JS is right to left, that is, the value is assigned to the variable on the left from the rightmost.
The above code is equivalent to

```javascript
var z = 1
z = typeof y;
var y = z;
console.log(y);
```

</p>
</details>

---

###### 16. What's the output?

```javascript
var foo = function bar(){ return 12; };
typeof bar();
```

<details><summary><b>Answer</b></summary>
<p>

#### Answer: Output is to throw an exception，bar is not defined

The code needs to be modified like this：

```javascript
var bar = function(){ return 12; };
typeof bar();
```
Or

```javascript
function bar(){ return 12; };
typeof bar();
```
Make it clear
```javascript
var foo = function bar(){
    // foo is visible here
    // bar is visible here
    console.log(typeof bar()); // Work here :)
};
// foo is visible here
// bar is undefined here
```
</p>
</details>

---

###### 17. What is the difference between the two function declarations?

```javascript
var foo = function(){
    // Some code
};
function bar(){
    // Some code
};
```

<details><summary><b>Answer</b></summary>
<p>

Foo is defined at run time. To illustrate this problem systematically, we need to introduce the concept of variable promotion.
We can run the following code to see the result.

```javascript
console.log(foo)
console.log(bar)

var foo = function(){
    // Some code
};
function bar(){
    // Some code
};
```
Output:

```javascript
undefined
function bar(){
    // Some code
};
```
Why? Why is foo printed as undefined and bar printed as a function?
When JavaScript executes, it promotes variables.
So the JavaScript engine in the above code executes in this order when actually executing.
```javascript

// The defined position of foo bar is raised
function bar(){
    // Some code
};
var foo;

console.log(foo)
console.log(bar)

foo = function(){
    // Some code
};
```

The output of the original code is reasonable.
</p>
</details>

---

###### 18. What's the output?

```javascript
var salary = "1000$";

(function () {
    console.log("Original salary was " + salary);

    var salary = "5000$";

    console.log("My New Salary " + salary);
})();
```

<details><summary><b>Answer</b></summary>
<p>
```javascript
Original salary was undefined
My New Salary 5000$
```
This question also examines variable promotion. Equivalent to the following code
```javascript
var salary = "1000$";

 (function () {
     var salary ;
     console.log("Original salary was " + salary);

     salary = "5000$";

     console.log("My New Salary " + salary);
 })();
 ```

</p>
</details>

---

###### 19. What is the instanceof operator? What does the following code output?

```javascript
function foo(){
  return foo;
}

console.log(new foo() instanceof foo);
```

<details><summary><b>Answer</b></summary>
<p>
The instanceof operator is used to determine whether the current object is an object of a specific class.
as

```javascript
function Animal(){
    //Or do not write the return statement
    return this;
}
var dog = new Animal();
dog instanceof Animal // Output : true
```
However, foo here is defined as
```javascript

function foo(){
  return foo;
}
```
so
```javascript

// here bar is pointer to function foo(){return foo}.
var bar = new foo();
```

调用foo的new foo（）instanceof foo返回 false

</p>
</details>

---

###### 20. If we use JavaScript "associative array", how can we calculate the length of "associative array"?

```javascript
var counterArray = {
    A : 3,
    B : 4
};
counterArray["C"] = 1;
```


<details><summary><b>Answer</b></summary>
<p>

`Object.keys(counterArray).length // Output 3`

</p>
</details>


