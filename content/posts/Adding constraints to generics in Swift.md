---
title: "Adding Constraints to Generics in Swift"
tags: ['Swift']
date:  2023-09-17
draft: false
---
Adding constraints to generics lets you narrow down what type of values you will be providing in your function while still maintaining the flexibility that generics allow.

In this example, I've added a constraint to Value that say whatever I pass in must conform to the Numeric protocol - meaning anything I pass to this function must be an array of integers, doubles, floats, or anything else that conforms to Numeric.

As long as whatever ever I pass in to this generic function conforms to Numeric, my function will be able to run successfully.

```swift
func count<Value: Numeric>(values: [Value]) {
    let total = values.reduce(0, +)
    print(total)
}

count(values: [2, 4, 6])
count(values: [2.21, 6.02, 10.82])
```
