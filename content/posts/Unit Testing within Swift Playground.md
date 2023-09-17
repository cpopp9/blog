---
title: "Unit Testing within Swift Playground"
tags: ['Swift', 'Unit Testing']
date:  2023-09-17
draft: false
---
Creating unit tests in Swift Playground is an easy way to double-check that you're getting the outcome you expect when developing new features.

In this example, I recreated the fizzbuzz challenge and ran it through multiple tests to ensure it was working as intended. The bottom line executes all of my tests within the FizzBuzzTests class.

```swift
import Foundation
import XCTest

class FizzBuzzTests: XCTestCase {
    
    let fizzArray = [3, 6, 9, 12, 18, 21, 24, 27]
    let buzzArray = [5, 10, 20, 25, 35, 40, 50, 55]
    let fizzbuzzArray = [15, 30, 45, 60, 75, 90, 105, 120]
    
    func testFizz() {
        for i in fizzArray {
            let result = fizzbuzz(number: i)
            XCTAssertEqual(result, "Fizz")
        }
    }
    
    func testBuzz() {
        for i in buzzArray {
            let result = fizzbuzz(number: i)
            XCTAssertEqual(result, "Buzz")
        }
    }
    
    func testFizzBuzz() {
        for i in fizzbuzzArray {
            let result = fizzbuzz(number: i)
            XCTAssertEqual(result, "FizzBuzz")
        }
    }
}

func fizzbuzz(number: Int) -> String {
    switch (number % 3 == 0, number % 5 == 0) {
    case (true, false):
        return "Fizz"
    case (false, true):
        return "Buzz"
    case (true, true):
        return "FizzBuzz"
    case (false, false):
        return String(number)
    }
}

FizzBuzzTests.defaultTestSuite.run()
```
