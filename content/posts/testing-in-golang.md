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

Before we dive in I'd like to cover some concepts quick

### Na, that is not a unit test!

What a unit and unittest is can vary. In our team, and in this blog, we do not see a unit as nessecarily corresponding 1:1 with a syntactic unit (class, function, stuct etc), but
can e.g. encompass one or more functions. A unit for us is more about what is solved, it can be a complex business operation or a simpe data format parsing. What a unit is is also
heavily dependent on the domain.

However, we do have a rather firm definition of what a unit test is; _a test that is not dependent on a external service, such as a database_. This means that even if we are
testing interaction with a database but mocking/stubbing that interaction out, it would count as a unittest.

### testify is king

Golang std lib for testing is somewhat lacking. The testify packages [assert](https://pkg.go.dev/github.com/stretchr/testify/assert) and
[require](https://pkg.go.dev/github.com/stretchr/testify/require) are really good and making testing a lot nicer!

### table driven tests

To test a bunch of different cases in golang a method commnly used is table driven tests. Essentially, you define what a test case is using an anonymous struct, then make an array
of test cases that you then loop over. It provides a simple and clean way to test

Here is an example how:

```go
package main

import (
	"testing"

	"github.com/stretchr/testify/assert"
	"github.com/stretchr/testify/require"
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
				require.NoError(t, err)
				assert.Equal(t, tc.want, got)
			}

		})
	}
}
```

## Part 1

```go
package main

type User struct {
	ID   string
	Name string
}


func NewUser(name string) (User, error) {
    if name == ""{
        return fmt.Errorf("username cannot be empty")
    }

    return User{
        ID: 123,
        Name: name
    }
}

type NewUserEvent struct {
	ID     string
	UserID string
}

type userRepo interface {
	Get(id string) (User, error)
	Insert(User) error
}

type eventQueue interface {
	Send(NewUserEvent) error
}

type UserService struct {
	repo userRepo
    eventQueue eventQueue
}

func (u UserService) RegisterNewUser(name string) error {
    user, err := NewUser(name)
    if err != nil {
        return err
    }

    err = repo.Insert(user)
    if err != nil {
        return err
    }


    err = repo.Insert(user)
    if err != nil {
        return err
    }

    err = eventQueue.Send()
    if err != nil {
        return err
    }


}

```

- Write story as going exploratory -> bad then -> improvements

### tabl

###

### defintion dependencies in test cases (what implements the interface)

### defintion evaluation in test case

#### Futher reading

- [Martin Fowler - Unit Test](https://martinfowler.com/bliki/UnitTest.html)
- [TableDrivenTest](https://go.dev/wiki/TableDrivenTests)
