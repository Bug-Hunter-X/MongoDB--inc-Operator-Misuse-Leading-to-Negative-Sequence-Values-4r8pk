# MongoDB $inc Operator Misuse
This repository demonstrates an uncommon error in using MongoDB's `$inc` operator within an update query.  The provided code incorrectly uses `$inc` to decrement a counter, potentially leading to unexpected negative values.  The solution shows the correct implementation for decrementing the counter using atomic operations.

## Bug Description
The `$inc` operator in MongoDB is intended for atomically incrementing numerical values.  While it seems intuitive to use a negative value with `$inc` to decrement,  this can cause issues if the counter reaches zero and then attempts to go negative.  This situation can arise from concurrent operations or a flawed application design, as it will never reach negative, instead it needs to be handled correctly.

## Solution
The solution utilizes a conditional update and the `$max` operator to achieve the desired outcome, ensuring the counter never goes below zero.