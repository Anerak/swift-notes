# **Swift Notes**

We can create a Playground environment in Xcode, remember to play "Run" to start your code and make changes.

## **Variables**

---

``` swift
var <variable name> = <value>
```

**Swift** is a type-safe language. That means it can distinct values.
It also means that we won't change an integer variable with a String value by mistake.

``` swift
var str = "Hey"
var age = 22
var population = 800_000
```

**Swift** allow us to use underscore to make big numbers more readable `(800000 = 800_000)`

Multi-line strings works with **`"""triple double quotes"""`**. The correct syntax is:

``` swift
var multi = """
Hello
"""
```

If we don't want line breaks inside our string, we finish each line with a backslash \

## **Types**

---

String  
 `var str = "Hello there"`

Integer  
 `var age = 22`

``` swift
Int and Double can't be mixed with operands.
```

Double  
 `var pi = 3.141`

Boolean  
 `var awesome = true`

String interpolation

All you have to do is write a backslash followed by parentheses surrounding the variable name.

``` swift
var score = 85
var str = "Your score is \(score)"
var str2 = "Hey there, did you know that 2 + 2 = \(2 + 2)"
```

Variables can change but **Swift** also offers constants.
The keyword is **`let`**

Type inference
We can be explicit about the type of our variable.

``` swift
//let <variable name>: <type> = <value>
let name: String = "Hello there"
let age: Int = 35
let pi: Double
```

## **Collection of values**

---

### **Arrays**

``` swift
let myArray = [1, 2, 3 ,4]
```

Arrays count from zero. **Swift** crashes to read an invalid offset.

If you're using type annotations, arrays are written in brackets.

``` swift
var cities: [String] = ["London", "Paris", "New York"]
```

#### Empty Array

There are two different ways.

``` swift
var integerArray = [Int]() // []
integerArray.append(5)     // [5]

var stringArray = Array<String>()
```

### **Sets**

They're like arrays but items aren't stored in any order.  
Items are unique. Duplicated values will be ignored.

We can create Sets from arrays

``` swift
let colors = Set(["red", "blue", "green"])
```

#### Empty Set

``` swift
var words = Set<String>()
```

### **Tuples**

They're like a `key-value` array. Allow us to store several values in a single value.

Tuples hold a fixed set of things that can't be changed (unlike dictionaries).  

``` swift
var name = (first: "Foo", last: "Bar")
name.0      // returns name.first : "Foo"
name.first // return "Foo"
```

### **Dictionaries**

Just like **`Tuples`** but more flexible.  
When using type annotations, dictionares are written in brackets with a colon betweeen your identifier and value types
**`[<key type>: <value type>]`**

**`Dicitionaries`** are so well optimized for store items, allowing a fast retrieval.

``` swift
let heights: [String: Double] = [
    "John Doe": 1.73,
    "Mr. X": 1.71,
    "Mrs. Y": 1.69,
]

print(heights["John Doe"]) // → 1.73
```

Unlike **`Tuples`**, you can't be guaranteed that a key in a dictionary exists.  
If you're trying to access an invalid offset of the dictionary, **`nil`** will be returned (equivalent of **`null`**).

We can define a `default` value for those situations.

``` swift
let favoriteColor: [String: String] = [
    "Foo"   : "red",
    "Mike"  : "blue",
    "John"  : "pink"
]

print(favoriteColor["Roy"]) // → nil
print(favoriteColor["Roy", default: "Unknown"]) // → "Unknown"
```

#### Empty Dictionary

``` swift
var scores = Dictionary<String, Int>()
scores["foo"] = 5
```

### Which one to choose?

* If you need a fixed collection of related values, use **Tuples**.
* If you need an unfixed collection of `key-value`, use **Dictionaries**
* If you need a collection of unique values, use **Sets**.
* If you need a collection with values that can repeat/order matters, use **Array**

### **Enums**

Sometimes we want to represent a value with a specific name. We can create **`enum`** to define those values.

``` swift
enum Result {
    case success
    case failure
}
var result = Result.success
```

**Swift** also allow us to associate values to **`enum`**

``` swift
enum Activity {
    case bored
    case running(destination: String)
    case talking(topic: String)
    case singing(volume: Int)
}

let talking = Activity.talking(topic: "sports")
```

**`enum`** can also generate numeric id for each case

``` swift
enum Planet: Int {
    case mercury = 1    // instead of 0, the id for this one will be 1
    case venus
    case earth
    case mars
}

let earth = Planet(rawValue: 2) // because mercury is 1, earth is 3

```

Make **`enums`** comparable by adding *`Comparable`* like `enum MyEnum: Comparable`

## **Operators and conditions**

---

### **Arithmetic operators**

``` swift
let firstScore = 12
let secondScore = 4
```

| Operator |Operation | Example | Result|Compound Assignment|
|----------|----------|---------|-------|-------------------|
|**`+`**| Addition  | `firstScore + secondScore` | `16` |**`+=`**|
|**`-`**|Substraction| `firstScore - secondScore` | `8` |**`-=`**|
|**`*`**|Multiply| `firstScore * secondScore` | `48` |**`*=`**|
|**`/`**|Division| `firstScore / secondScore` | `3` |**`/=`**|
|**`%`**|Division Remainder| `firstScore % secondScore` | `0` |**`%=`**|

### **Operator overloading**

It consist on the posibility of operating based on the type of data:

``` swift
let lifeNumber = 42
let doubleLife = 42 + 42
// → 84

let fakers = "Fakers gonna "
let action = fakers + "fake"
// → "Fakers gonna fake"

let firstHalf = ["John", "Paul"]
let secondHalf = ["George", "Ringo"]
let beatles = firstHalf + secondHalf

// → ["John", "Paul", "George", "Ringo"]
```

### **Comparison operators**

``` swift
let firstScore = 6
let secondScore = 4
```

| Operator | Operation       | Example                    |Result|
|----------|-----------------|----------------------------|---------|
| **`==`** |equals           | `firstScore == secondScore` | **`false`**
| **`!=`** |different        | `firstScore != secondScore` | **`true`**
| **`>`**  |greater than     | `firstScore > secondScore` | **`true`**
| **`>=`** |greater or equals| `firstScore >= secondScore` | **`true`**
| **`<`**  |lesser than      | `firstScore < secondScore` | **`false`**
| **`<=`** |lesser or equals | `firstScore <= secondScore` | **`false`**
|**`&&`**  |and              | `true && false` | **`false`**
|**`||`**  |or               | `true || false` | **`true`**

### **Conditions**

Mainly, the **`if`** and **`else`** statements.

Parentheses aren't part of the syntax style but they can be used for read purposes. Also, it will help **Swift** to understand what's the order of conditions.

``` swift
let name: String = "Foo"

if name == "Bar" {
    print("The name is Bond. \(name) Bond.")
} else if name == "Foo" {
    print("This guy is called \(name).")
} else {
    print("We don't know your name.")
}
```

### **Ternary operator**

``` swift
let firstCard = 11
let secondCard = 10

// <condition> ? <true> : <false>

print(firstCard == secondCard ? "Cards are the same" : "Cards are different")
```

### **`switch`**

Check a value against multiple values.

Use **`fallthrough`** for continue the execution on the next case.

``` swift
let weather = "sunny"

switch weather {
    case "rain":
        print("Bring an umbrella)
    case "snow":
        print("Wrap up warm")
    case "sunny":
        print("Wear sunscreen")
        fallthrough
    default:
        print("Have a nice day")
}

```

### **Range operators**

Useful to check if a numeric value exists on a range.

``` swift
let foo: Int = 5

switch foo {
    case 0..<10:
        print("Between 0 and 9")
    case 10..20
        print("Between 10 and 20")
    default:
        print("Meh")
}
```

| Operator  |           Operation             |   Example
|-----------|---------------------------------|---------------------|
| **`..<`** |from to less than                | `1..<5 → 1 2 3 4` |
| **`...`** |from to including the last number| `1...5 → 1 2 3 4 5` |

## **Loops**

---

### **`for`** **loops**

Useful to loop over a collection or generating stuff.

``` swift
let count = 1...10

for number in count {
    print("Number is \(number)")
}
// → "Number is 1", "Number is 2"...

let albums = ["The Big DB", "CPU-to-Core 2", "Pear"]
for album in albums {
    print("\(album) is on Orange Music")
}
// → "The Big DB is on Orange Music", "CPU-to-Core 2 is on Orange Music"...
```

If we don't use the constant that **`for`** give us, we should use an underscore to avoid creating needless values.

``` swift
print("Are you ready to...")

for _ in 1...5 {
    print("play")
}
```

### **`while`** *loops*

It will loop as long the condition is true

``` swift
var number = 1
while number <= 20 {
    print(number)
    number += 1
}
print("I'm done here")
```

### **`repeat`** **loops**

Like **`while`** but it will run at least once before checking if the condition is true.

``` swift
var number = 1
repeat {
    print(number)
    number += 1
} while number <= 20
```

### **Exiting loops**

Use the **`break`** keyword to exit a loop before it finish.

``` swift
while true {
    print("Hello")
    break
}
```

What about nested loops?  
We can define a name for the outer loop ( `labeled statements` ), so we stop that one, stopping the inner loop at the same time.

Then, we make use of the **`break`** keyword followed by the name of the outer loop.

``` swift
outerLoop: for i in 1...10 {
    for j in 1...10 {
        let product = i * j
        print("\(i) * \(j) is \(product)")
        if product == 50 {
            break outerLoop
        }
    }
}
```

### **Skipping items**

The keyword here is **`continue`**

``` swift
for i in 0...10 {
    if i % 2 == 0 {
        continue
    }
    print(i)
}
// → 1 3 5 7 9
```

## **Functions**

---

Wrap pieces of code for being used in lots of places.

### **`Very helpful to avoid code duplication`**

**Swift** uses the **`func`** keyword.

``` swift
func sayHi() {
    let message = "Hello"
    print(message)
}

sayHi()
// → "Hello"
```

### **Function Arguments**

Let your function receive arguments by adding the name followed by the type between parentheses.

``` swift
func square(number: Int) {
    print(number * number)
}
square(number: 9)
// → 81
```

### **Returning Data**

We need to define which type of data our function will return.

``` swift
func square(number: Int) -> Int /* type of data returned */ {
    return number * number
}
```

Remember that functions have a single return type. If you want to return more than one value, use a tuple, an array or some other type of collection.  
It's recommended to use a tuple because we can define the name of the values we're returning.

``` swift
func getUser() -> (first: String, last: String) {
    (first: "John", last: "Doe")
}

let user = getUser()
print(user.first)
// → "John"
```

Also, if our function has only one line, we don't need the **`return`** keyword. It means that you require a **`return`** if the function contains an if or any other code. Ternary operator is an exception.

``` swift
func randomFn(n: Int) -> Int {
    n + 2
}
```

### **Labeled Arguments**

**Swift** allow us to label arguments, giving them one name for calling the function and another for internal use.

``` swift
func sayHello(to name: String) {
    print("Hello, \(name)")
}

sayHello(to: "Foobar")
// → "Hello, Foobar"
```

### **Unlabeled Arguments**

Let's say we don't want to name our parameter, making it more like `greet("Foo")` .  
In order to achieve this behavior, we need to call our parameter **`_`** underscore.

``` swift
func greet(_ person: String) {
    print("Hello, \(person)!")
}

greet("Foo")
// → "Hello, Foo"
```

### **Default Parameters**

In case we want an argument to have a default value, we just assign it while we're defining it.

``` swift
func greet(_ person: String, nicely: Bool = true) {
    if (nicely == true) {
        print("Hello, \(person)")
    } else {
        print("You again, \(person)")
    }
}
greet("Foo")
// → "Hello, Foo"
greet("Bar", nicely: false)
// → "You again, Bar"
```

### **Variadic Functions**

We can create a function that receives many values of the same type as an argument. **Swift** will convert those values into an array that we can iterate over.

Add **`...`** to the parameter to convert it into a variadic parameter.

``` swift
func square(numbers: Int...) {
    for n in numbers {
        print("\(n) squared is \(n * n)")
    }
}

square(numbers: 1, 2, 3, 4, 5)

```

### **Throwing Functions**

Sometimes funtions fail because they have bad input or something went wrong internally.

We can mark functions as **`throws`** before their return type, then using the **`throw`** keyword when something goes wrong.

First we define an **`enum`** that describes the errors we can throw. These must always be based on **Swift**'s existing **`Error`** type.

``` swift
enum PasswordError: Error {
    case obvius
}

func checkPassword(_ password: String) throws -> Bool {
    if password == "password" {
        throw PasswordError.obvius
    }
    return true
}
```

In order to run an error-throwing function, we need to use the **`do`**, **`try`** and **`catch`** keywords.

**`do`** starts a section of code that might cause problems.

``` swift
do {
    try checkPassword("password")
    print("That password is good")
} catch {
    print("You can't use that password")
}
```

### **Intout parameters**

All parameters sent to a function are defined as constants, that means it can't change. That's when the **`inout`** keyword comes handy.

The **`inout`** keyword for arguments is used to determine that the variable you sent to the functon, can be changed during the execution of the function.

``` swift
func doubleInPlace(number: inout Int) {
    number += 2
}

var myNum = 10
doubleInPlace(number: myNum)
```

To use this function, you can't use constants as parameters.

The ampersand **`&`** symbol must be included before the name of the argument as a confirmation that we are using an **`inout`** parameter.

## **Closures**

---

Apparently, this should be hard to understand, so buckle up, buckaroo!

### **Basic example**

Like defining a variable or a constant, requires a **`var`** or **`let`** keyword.

``` swift
let driving = {
    print("I'm driving in my car")
}

driving()
// → "I'm driving in my car"

var meCool = {
    print("Yes, I'm cool")
}

meCool()
// → "Yes, I'm cool"

```

### **Closure Arguments**

Unlike functions, the parentheses for arguments goes inside the curly braces, followed by the keyword **`in`**. The reason is to avoid confusing **Swift** by making it think that we're defining a tuple.

**Keep in mind that `closures` can't make use of labeled arguments**

``` swift
let driving = { (place: String) in
    print("I'm going to \(place) in my car")
}

driving("Europe")
// → "I'm going to Europe in my car"
```

### **Returning values**

Just like a normal function, we need to declare the type of data our closure will return.

``` swift
let checkEven = { (number: Int) -> Bool in
    if number % 2 == 0 {
        return true
    }
    return false
}

checkEven(6)
// → true

let noParameters = { () -> Bool in
    print("This takes no parameters")
    return true
}
noParameters()
// → "This takes no parameters"
// → true

```

### **Using closures as parameters**

We may find situations where one of the arguments for our functions is a closure (**SwiftUI** relies heavily on this).  
In order to take a closure as argument, we must declare it's type as `() ->` followed by the return type.

``` swift

let driving = {
    print("I'm driving in my car")
}

func travel(action: () -> Void) {
    print("I'm getting ready to go")
    action()
    print("I arrived")
}

travel(action: driving)
// → "I'm getting ready to go"
// → "I'm driving in my car"
// → "I arrived"
```

### **Trailing closure syntax**

A function which last (or only) argument is a closure, can be written with a different syntax.

``` swift
func functionWithClosure(action: () -> Void) {
    print("This goes first")
    action()
    print("This goes last")
}

functionWithClosure() {
    print("Option 1. Useful when there's more parameters")
}
// → "This goes first"
// → "Option 1. Useful when there's more parameters"
// → "This goes last"

functionWithClosure {
    print("Option 2. Useful when only the closure is the parameter")
}
// → "This goes first"
// → "Option 2. Useful when only the closure is the parameter"
// → "This goes last"
```

### **Closures with parameters as parameters**

We use a closure as a parameter but that very same closure also accepts parameters.  
In our function, when we declare the closure as an argument, the parentheses must contain the type of argument that it takes.

``` swift
func travel(action: (String) -> Void) {
    print("I'm getting ready to go.")
    action("London")
    print("I arrived.")
}

travel { (place: String) in
    print("I'm going to \(place) in my car.")
}
// → "I'm getting ready to go."
// → "I'm going to London in my car."
// → "I arrived."
```

### **Closures with return values as parameters**

What happens if our closure returns a value? What do we do?  
Well, just save it into a **`var`** / **`const`** or pass it into another function.

``` swift
func getRich(action: (String) -> String) {
    print("( 1 ) Learn Swift")
    let middleStep = action("2")
    print(middleStep)
    print("( 3 ) Profit!")
}

getRich { (step: String) -> String in
    return "( \(step) ) ???"
}
// → "( 1 ) Learn Swift"
// → "( 2 ) ???"
// → "( 3 ) Profit!"
```

### **Shorthand closure syntax**

If we have something like this

``` swift
func doSomething(action: (String) -> String) {
    let fun = action("jump")
    print(fun)
}

doSomething { (verb: String) -> String in
    return "Let's \(verb)!"
}
// → "Let's jump!"
```

We can take advantage of **Swift** to simplify the closure.

``` swift

//    Swift knows what parameter type the closure needs,
//    then we can remove the type.

doSomething { verb -> String in
    return "Let's \(verb)"
}

// Swift knows that we are returning a String.
// Also, convert it into a one-liner and remove the return keyword.
doSomething { verb in
    "Let's \(verb)"
}

// And finally, we can replace the argument part by using $0
// 0 belongs to the first parameter, it's auto-incremental.
travel {
    "Let's \($0)"
}
```

### **Closures with multiple arguments**

``` swift
func obeyMe(action: (String, Int) -> String) {
    let order = action("jump", 60)
    print(order)
}

obeyMe {
    "I'm going to \($0) at least \($1) times."
}
// → "I'm going to jump at least 60 times."
```

### **Returning closures from functions**

Perhaps a little bit tricky because we must use **`->`** twice. One for the function's return value and another one for the closure's return value.

``` swift
func travel() -> (String) -> Void {
    return {
        print("I'm going to \($0)")
    }
}

let result = travel()
result("London")
// → "I'm going to London"

// Allowable but definitely NOT recommended.
let result2 = travel()("London")
// → "I'm going to London"
```

### **Capturing values**

Variables inside closures keep their value even after the code executed.

That means that the value of a `counter` variable will be the same as left when you executed the closure for the first time (unless you reset it).

## **`structs`**

---
**Swift** let us design our own types in two ways, the most common one is called **`struct`**

Tuples can be seen as anonymous structs but think about all the work you must do to add a new property.

Constants can't be properties.

``` swift
struct Sport {
    var name: String
}

var tennis = Sport(name: "Tennis")
print(tennis.name)
// → "Tennis"

tennis.name = "Lawn tennis"
print(tennis.name)
// → "Lawn tennis"
```

### **Computed properties**

The properties we store inside the **`struct`** using something like `var name: String` or `var foo = "Bar"` are called *`stored`* properties.  
On the other hand, we can define *`computed`* properties, which value will be set accordingly on the return value of our code.

``` swift
struct Sport {
    var name: String
    var isOlympicSport: Bool

    var olympicStatus: String {
        if isOlympicSport {
            return "\(name) is an Olympic sport"
        } else {
            return "\(name) is not an Olympic sport"
        }
    }
}

let chessBoxing = Sport(name: "Chessboxing", isOlympicSport: false)
print(chessBoxing.olympicStatus)
// → "Chessboxing is not an Olympic sport"
```

### **Property observers**

Run code before or after any property changes.  
Use **`didSet`** for run code after the property has been changed or **`willSet`** to run code before the property changes.

``` swift
struct Progress {
    var task: String
    var amount: Int {
        didSet {
            print("\(task) is now \(amount)% complete.")
        }
    }
}

var progress = Progress(task: "Loading data", amount: 0)
progress.amount = 30
// → "Loading data is now 30% complete."
progress.amount = 80
// → "Loading data is now 80% complete."
progress.amount = 100
// → "Loading data is now 100% complete."

```

### **`struct`** **methods**

A **`struct`** can have functions inside, called methods but still uses the **`func`** keyword.

``` swift
struct City {
    var population: Int

    func collectTaxes() -> Int {
        return population * 1000
    }
}

let london = City(population: 9_000_000)
london.collectTaxes()
// → 9000000000
```