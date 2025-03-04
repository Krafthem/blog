+++
author = 'Axel Almquist'
date = '2025-03-03T13:35:44+01:00'
draft = true
title = 'Testing in Golang'
+++

# Testing in Golang

During the last two year while moving to golang we gone threw a few interation of how to test things.

In this post ill go over our testing journey. In this post we will focus on unit testing.

## prelude

Before we start I'd just like to cover some small concepts quick

### Na, that is not a unit test?

Before we dive in i'd also like to quickly mention what we refer to as a unit test. We define a unit rather lossely as 'any unit of work that is indepenent of a external system
during testing". For example, this would not cover tests where we testing stuff that is hitting a running postgres db (setup in docker or whatever), but pretty much anything else;
testing a small utility funciton or testing a larger unit of work involing many functions or/and structs.

### table driven tests

To test a bunch of different cases in golang a method commnly used is table driven tests. Essentially, you define what a test case is using an anonymous struct, then make an array
of test cases that you then loop over. It provides a simple and clean way to test

Here is an example how:

```go
package main

import (
	"testing"

	"github.com/stretchr/testify/assert"
)

func SomeFunc(input string) (string, error) {
	return "some data", nil
}

func TestExample(t *testing.T) {

	testCases := []struct {
		name        string
		input       string
		want        string
		expectError bool
	}{
		{
			name:  "happy - test case 1",
			input: "some input",
			want:  "some output",
		},

		{
			name:        "happy - test case 2",
			input:       "some input",
			expectError: true,
		},
	}

	for _, tc := range testCases {
		t.Run(tc.name, func(t *testing.T) {

			got, err := SomeFunc(tc.input)
			if tc.expectError {
				assert.Error(t, err)
			} else {
				assert.NoError(t, err)
				assert.Equal(t, tc.want, got)
			}

		})

	}

}
```

## MAIN

- Write story as going exploratory -> bad then -> improvements

### tabl

###

### defintion dependencies in test cases (what implements the interface)

### defintion evaluation in test case

#### Futher reading

- [Martin Fowler - Unit Test](https://martinfowler.com/bliki/UnitTest.html)
- [TableDrivenTest](https://go.dev/wiki/TableDrivenTests)
