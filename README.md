# Closures lab 1

Fork and clone this repo. On your fork, answer and commit the follow questions. When you are finished, submit the link to your repo on Canvas.

## Question 1

Write a function named `applyKTimes` that takes an integer `K` and a closure and calls the closure K times. The closure will not take any parameters and will not have a return value.

Function Definition:
func applyKTimes(_ K: Int, _ closure: () -> ())

Example:
Input:

```swift
applyKTimes(3) {
    print("We Heart Swift")
}
```
Output:

```swift
We Heart Swift
We Heart Swift
We Heart Swift
```

```swift
func applyKTimes(_ K: Int, _ closure: () -> ()) {
    for _ in 1...K {
        closure()
    }
}

applyKTimes(2) {
    print("Closures are lit!")
}
```

## Question 2

Use `filter` to create an array called `multiples` that contains all the multiples of 3 from `numbers` and then print it.

`let numbers = [1, 2, 3, 4, 6, 8, 9, 3, 12, 11]`

Example:
Input: `let numbers = [1, 2, 3, 4, 6, 8, 9, 3, 12, 11]`

Expected values: `multiples = [3, 6, 9, 3, 12]`

```swift
let numbers = [1, 2, 3, 4, 6, 8, 9, 3, 12, 11]

let multiples = numbers.filter({ $0 % 3 == 0})

print(multiples)
```

## Question 3

Find the largest number from `numbers` and then print it. Use `reduce` to solve this exercise.

Example:
Input: `let numbers = [4, 7, 1, 9, 6, 5, 6, 9]`

Output: `9`

```swift
let numbers = [4, 7, 1, 9, 6, 5, 6, 9]

let largestNumber = numbers.reduce(0, {
    $0 > $1 ? $0 : $1
})
print(largestNumber)
```

## Question 4

Join all the strings from `strings` into one using `reduce`. Add spaces in between strings. Print your result.

Example:
Input: `let strings = ["We", "Heart", "Swift"]`

Output: `"We Heart Swift"`

```swift
let strings = ["We", "Heart", "Swift"]

let singleString = strings.reduce(into:"", {
    $0 += "\($1) "
}).dropLast()

print(singleString,".", separator: "")
```

## Question 5

`let cities = ["Shanghai", "Beijing", "Delhi", "Lagos", "Tianjin", "Karachi", "Karachi", "Tokyo", "Guangzhou", "Mumbai", "Moscow", "São Paulo"]`

a. Use `sortedBy` to sort `cities` in alphabetical order.

b. Use `sortedBy` to sort `cities` alphabetical order of the second character of the city name.

c. Use `sortedBy` to sort `cities` in order of the length of the city name.

```swift
let cities = ["Shanghai", "Beijing", "Delhi", "Lagos", "Tianjin", "Karachi", "Karachi", "Tokyo", "Guangzhou", "Mumbai", "Moscow", "São Paulo"]

// Use `sortedBy` to sort `cities` in alphabetical order.
let alphabeticalOrder = cities.sorted(by: <)
print("Sorted by alphabetical order of the city name:",alphabeticalOrder, separator: "\n",terminator: "\n\n")

// Use `sortedBy` to sort `cities` alphabetical order of the second character of the city name.
let secondLetterAlphabeticalOrder = cities.sorted(by: { x, y in
    Array(x)[1] < Array(y)[1]
})
print("Sorted by alphabetical order of the second character in city name:",secondLetterAlphabeticalOrder, separator: "\n",terminator: "\n\n")

// Use `sortedBy` to sort `cities` in order of the length of the city name.
let lengthOfCityName = cities.sorted(by: { x, y in
    x.count > y.count
})
print("Sorted by the length of the city name:",lengthOfCityName, separator: "\n",terminator: "\n\n")
```

## Question 6

`let citiesWithPopulation: [(String, Int)] = [("Shanghai", 24256800), ("Beijing", 21516000), ("Delhi", 16787941), ("Lagos", 16060303), ("Tianjin", 15200000), ("Karachi", 14910352), ("Karachi", 14160467), ("Tokyo", 13513734), ("Guangzhou", 13080500), ("Mumbai", 12442373), ("Moscow", 12380664), ("São Paulo", 12038175)]`

a. Use `sortedBy` to sort `citiesWithPopulation` in ascending order of population.

b. Use `sortedBy` to sort `citiesWithPopulation` in reverse alphabetical order of the last character in the city name.

```swift
let citiesWithPopulation: [(String, Int)] = [("Shanghai", 24256800), ("Beijing", 21516000), ("Delhi", 16787941), ("Lagos", 16060303), ("Tianjin", 15200000), ("Karachi", 14910352), ("Karachi", 14160467), ("Tokyo", 13513734), ("Guangzhou", 13080500), ("Mumbai", 12442373), ("Moscow", 12380664), ("São Paulo", 12038175)]

// Use `sortedBy` to sort `citiesWithPopulation` in ascending order of population.
let orderOfPopulation = citiesWithPopulation.sorted(by: { x, y in
    x.1 < y.1
})
print("Sorted by order of population:",orderOfPopulation, separator: "\n",terminator: "\n\n")

// Use `sortedBy` to sort `citiesWithPopulation` in reverse alphabetical order of the last character in the city name.
let reverseAlphabeticalOrderOfTheLastChar = citiesWithPopulation.sorted(by: {x, y in
    Array(x.0)[x.0.count - 1] > Array(y.0)[y.0.count - 1]
})
print("Sorted by alphabetical order of the last character in the city name:",reverseAlphabeticalOrderOfTheLastChar, separator: "\n",terminator: "\n\n")
```

## Question 7

Sort `numbers` in ascending order by the number of divisors. If two numbers have the same number of divisors the order in which they appear in the sorted array does not matter.

`var numbers = [1, 2, 3, 4, 5, 6]`

Example:
Input: `var numbers = [1, 2, 3, 4, 5, 6]`

Output:

```swift
numbers = [1, 2, 3, 5, 4, 6]
// 1 has one divisor
// 2, 3 and 5 have 2
// 4 has 3 divisors
// 6 has 4 divisors

// [1, 5, 2, 3, 4, 6] would also have been a valid solution
```

```swift
var numbers = [1, 2, 3, 4, 5, 6,7]

let sortByNumberOfDivisors = { (arr: [Int] ) -> [Int] in
    var outputArray = [Int]()
    var divisorCountTuple = [(number: Int , count: Int)]()

    for number in arr {
        var numberOfDivisors = 0
        for x in 1...number where number % x == 0{
            numberOfDivisors += 1
        }
        divisorCountTuple.append((number: number, count: numberOfDivisors))
    }
    divisorCountTuple.sort(by: {(x,y) in
        x.count < y.count
    })

    for (number, _) in divisorCountTuple {
        outputArray.append(number)
    }
    return outputArray
}

print(sortByNumberOfDivisors(numbers))
```


## Question 8

Find the sum of the squares of all the odd numbers from `numbers` and then print it.

`var numbers = [1, 2, 3, 4, 5, 6]`

a. Write code that removes all the odd numbers from the array.

b. Write code that squares all the numbers in the array.

c. Write code that finds the sum of the array.

d. Now use `map`, `filter` and `reduce` to solve this problem.

Example:
Input: `var numbers = [1, 2, 3, 4, 5, 6]`

Output: `35 // 1 + 9 + 25 -> 35`

```swift
var numbers = [1, 2, 3, 4, 5, 6]
print("Numbers array:", numbers, separator: "\n", terminator: "\n\n")

// Write code that removes all the odd numbers from the array.
var allEvenNumbers = [Int]()
for number in numbers where number % 2 != 1 {
    allEvenNumbers.append(number)
}
print("Removed all odd numbers from the numbers array using for loops:", allEvenNumbers, separator: "\n", terminator: "\n\n")

// Write code that squares all the numbers in the array.
var squareOfAllNumbers = [Int]()
for number in numbers {
    squareOfAllNumbers.append(number * number)
}
print("Squared all the numbers in the numbers array using for loops:", squareOfAllNumbers, separator: "\n", terminator: "\n\n")

// Write code that finds the sum of the array.
var sumOfAllNumbersInTheArray = 0
for number in numbers {
    sumOfAllNumbersInTheArray += number
}
print("Sum of all the numbers in the numbers array using for loops:", sumOfAllNumbersInTheArray, separator: "\n", terminator: "\n\n")

// Write code that removes all the odd numbers from the array.
let noOddNumbers = numbers.filter({ $0 % 2 != 01 })
print("Removed all the odd numbers using filter:",noOddNumbers, separator: "\n", terminator: "\n\n")

// Write code that squares all the numbers in the array.
let numbersSquared = numbers.map({$0 * $0})
print("Squared all the numbers using map:",numbersSquared, separator: "\n", terminator: "\n\n")

// Write code that finds the sum of the array.
let sumNumbers = numbers.reduce(0, {$0 + $1})
print("Sum of numbers in the array using reduce:",sumNumbers, separator: "\n", terminator: "\n\n")
```

## Question 9

Implement a function `forEach(array: [Int], _ closure: Int -> ())` that takes an array of integers and a closure and runs the closure for each element of the array.

Example:
Function with Input:

```swift
forEach([1, 2, 3, 4]) {
    print($0 * $0)
}
```

Output:

```swift
1
4
9
16
```

```swift
func forEach(_ array: [Int], _ closure: (Int) -> ()) {
    for number in array {
        closure(number)
    }
}

forEach([1, 2, 3, 4]) {
    print($0 * $0)
}
```


## Question 10

Create a closure that takes one Int and returns the doubled value. Check by passing the closure's return to a variable.

```swift
let doubleInt = {(a: Int) -> Int in
    return a * 2
}

print(doubleInt(3))
```

## Question 11

Create a closure that takes one Int and returns a bool whether or not it's divisible by 3.

```swift
let isDiv3 = { (a: Int) -> Bool in
    return a % 3 == 0
}
print(isDiv3(6))
```

## Question 12

Create a closure that takes two strings as input and returns the longest character count of the two strings.

```swift
let largerStringCount = { (str1: String, str2: String) -> String in
    return str1.count >= str2.count ? "The longest string has a character count of: \(str1.count)" : "The longest string has a character count of: \(str2.count)"
}
print(largerStringCount("This is string 1.", "String 2"))
```

## Question 13

Create a closure that takes an array of Int as input and returns the largest element in the array

```swift
let largestElementInArray = { (array: [Int]) -> Int in
    var currentMax = Int.min
    for number in array where number > currentMax {
        currentMax = number
    }
    return currentMax
}
print(largestElementInArray([2,4,1,6,3,4,1,2,8,5,10]))
```

## Question 14

Create a closure that takes an array of Int and variable x: Int as input and returns the xth largest element in the array. Assume x is always < the count of the array.

Write a new closure like the one above and add handling for cases where x >= the count of the array (Hint: Use optionals)

```swift
let nthLargestNumberInArray = { (arr: [Int], x: Int) -> Int in
    var sortedArray = arr.sorted(by: >)
    return sortedArray[x - 1]
}
print(nthLargestNumberInArray([1,2,3,4,5,6,7,8,9,10], 1))
```

## Question 15

Write a closure that compares two numbers, and determines whether the first number's square is bigger than the second number cubed, then use it to sort this array.

Example:
Input: `[41, 4, -4, -100, 24, 61, -3, -2, -1]`

Output: `[-4, 4, -100, -3, -2, -1, 61, 24, 41] // this is a little weird!`

```swift
let biggerSquareSort = {(arr: [Int]) -> [Int] in
    return arr.sorted(by: {
        $0 * $0 < $1 * $1 * $1
    })
}
print(biggerSquareSort([41, 4, -4, -100, 24, 61, -3, -2, -1]))
```

## Question 16

Write a function that takes in an [Int?] and a closure or function as parameters and returns an [Int]. The closure should take in an Int? and return a Bool.

This function should run all the Int?s through the closure, which determines if the value can be unwrapped. Then, unwrap all elements that aren't nil in your main function to return in an Array.

Example:
Input: `let optionalIntArray = [1, 2, nil, 4, 5, nil, 7, 8]`

Output: `[1, 2, 4, 5, 7, 8]`

```swift
let optionalIntArray = [1, 2, nil, 4, 5, nil, 7, 8]

let unwrappedArray = { (arr: [Int?]) -> [Int] in
    var outputArray = [Int]()
    for optionalNumber in arr {
        if let number = optionalNumber {
            outputArray.append(number)
        }
    }
    return outputArray
}
print(unwrappedArray(optionalIntArray))
```

## Question 17

Write a decoding function that takes an [Int?] and decodes it according to the number's place in the alphabet. (ex. 1 = a, 2 = b, 26 = z)

Requirement: This function takes in an [Int?] and a closure or function as parameters and returns a String. The closure should take in an Int? and return a Character if there is a value and a space if it's nil.

Use this out of scope of your function:

```swift
var alphaDict = [Int : Character]()
for (x,y) in "abcdefghijklmnopqrstuvwxyz".enumerated() {
 alphaDict[x+1] = y
}
```

Input: `let optionalIntArray = [1, 12, 12, nil, 2, 5, 14, 19, nil, 6, 1, 21, 12, 20]`

```swift
let optionalIntArray = [1, 12, 12, nil, 2, 5, 14, 19, nil, 6, 1, 21, 12, 20]

var alphaDict = [Int : Character]()
for (x,y) in "abcdefghijklmnopqrstuvwxyz".enumerated() {
    alphaDict[x+1] = y
}
let decodedMessage = { (arr: [Int?]) -> String in
    var outputString = ""
    for optionalNumber in  arr {
        if let number = optionalNumber , let character = alphaDict[number]{
            outputString.append(character)
        } else {
            outputString += " "
        }
    }
    return outputString
}
print(decodedMessage(optionalIntArray))
```
