# CPP Module 08

This repository contains my implementation of **C++ Module 08**, developed as part of the 42 School curriculum. This module introduces the Standard Template Library (STL), focusing on templated containers, iterators, and algorithms - the fundamental building blocks of modern C++ programming.

**"Templated containers, iterators, algorithms"**

## Table of Contents

- [Overview](#overview)
- [General Rules](#general-rules)
- [Module-Specific Rules](#module-specific-rules)
- [Exercises](#exercises)
  - [Exercise 00: Easy find](#exercise-00-easy-find)
  - [Exercise 01: Span](#exercise-01-span)
  - [Exercise 02: Mutated abomination](#exercise-02-mutated-abomination)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Submission and Peer Evaluation](#submission-and-peer-evaluation)
- [Acknowledgments](#acknowledgments)
- [Disclaimer](#disclaimer)
- [License](#license)

## Overview

C++ is a general-purpose programming language created by **Bjarne Stroustrup** as an extension of the C programming language, or "C with Classes". This module marks an important milestone: the introduction of the **Standard Template Library (STL)**, which provides powerful, reusable components for data structures and algorithms.

Key topics covered in this module:
- **STL Containers** - vector, list, map, stack, and other data structures
- **Iterators** - objects that provide sequential access to container elements
- **Algorithms** - standard functions for searching, sorting, manipulating data
- **Container adaptors** - specialized interfaces built on top of containers
- **Range-based operations** - working with sequences of elements
- **Iterator categories** - understanding different types of iterators

All exercises must be written in **C++98** and compiled using the appropriate flags.

**Important:** Starting from this module, you MUST use STL containers and algorithms whenever appropriate. Not using them will result in a poor grade.

## General Rules

- **Compilation:**
  - Compile with `c++ -Wall -Wextra -Werror`
  - Code must still compile with `-std=c++98`

- **Formatting & Naming:**
  - Exercises are stored in directories `ex00`, `ex01`, `ex02`, …  
  - Class names in `UpperCamelCase` (e.g., `Span`, `MutantStack`)  
  - Source files: `ClassName.cpp`  
  - Header files: `ClassName.hpp` or `ClassName.h`
  - Template implementation files: `ClassName.tpp` (optional)

- **Allowed / Forbidden:**
  - **NOW ALLOWED:** STL Containers (vector, list, map, etc.) and Algorithms
  - Forbidden: external libraries, C++11 or newer, Boost libraries
  - Forbidden functions: `*printf()`, `*alloc()`, `free()`
  - Forbidden keywords: `using namespace <ns_name>`, `friend` (unless explicitly stated)

- **Design Requirements:**
  - All classes must follow the Orthodox Canonical Form (unless stated otherwise)
  - Avoid memory leaks when using `new` / `delete`
  - Each header must be self-contained and protected by include guards
  - Function implementations in headers allowed ONLY for templates

## Module-Specific Rules

**CRITICAL:** While exercises CAN be solved without STL containers and algorithms, the goal is to USE them as much as possible.

- **Use STL Containers** - vector, list, map, stack, etc.
- **Use STL Algorithms** - find, sort, copy, transform, etc. (from `<algorithm>`)
- Apply them wherever appropriate
- Using them demonstrates understanding of modern C++ practices

**You will receive a poor grade if you don't use STL components, even if your code works.**

Template implementations can be:
- Written directly in header files, OR
- Declared in `.hpp` and implemented in `.tpp` files

## Exercises

### Exercise 00: Easy find

**Directory:** `ex00/`  
**Files to turn in:** `Makefile`, `main.cpp`, `easyfind.{h,hpp}` and optional `easyfind.tpp`

Create a function template that finds a value in a container of integers.

**Function template:**
```cpp
template<typename T>
??? easyfind(T& container, int value);
```

**Parameters:**
- `container` - a container of type T (must contain integers)
- `value` - the integer to find

**Behavior:**
- Finds the first occurrence of `value` in `container`
- If found: return appropriate value (iterator, index, etc.)
- If not found: throw exception or return error value

**Requirements:**
- Works with any STL container of integers
- Does NOT need to handle associative containers (map, set)
- Use STL algorithms where appropriate

**Example usage:**
```cpp
std::vector<int> vec;
vec.push_back(1);
vec.push_back(2);
vec.push_back(3);

easyfind(vec, 2);  // Should find 2
easyfind(vec, 5);  // Should throw or return error
```

**Key Learning:** Function templates with containers, STL algorithms (std::find), iterator handling, exception handling.

### Exercise 01: Span

**Directory:** `ex01/`  
**Files to turn in:** `Makefile`, `main.cpp`, `Span.{h,hpp}`, `Span.cpp`

Develop a `Span` class that stores a maximum of N integers and can compute spans.

**Class design:**
```cpp
class Span {
public:
    Span(unsigned int N);  // Constructor with max capacity
    void addNumber(int number);
    int shortestSpan();
    int longestSpan();
};
```

**Member functions:**

**addNumber()**
- Adds a single number to the Span
- Throws exception if already N elements stored

**shortestSpan()**
- Returns the shortest span between any two stored numbers
- Throws exception if less than 2 numbers stored

**longestSpan()**
- Returns the longest span between any two stored numbers  
- Throws exception if less than 2 numbers stored

**Additional requirement:**
Implement a way to add multiple numbers using a **range of iterators** in a single call.

**Example usage:**
```cpp
Span sp = Span(5);
sp.addNumber(6);
sp.addNumber(3);
sp.addNumber(17);
sp.addNumber(9);
sp.addNumber(11);

std::cout << sp.shortestSpan() << std::endl;  // Output: 2
std::cout << sp.longestSpan() << std::endl;   // Output: 14
```

**Testing requirements:**
- Test with at least 10,000 numbers
- Test iterator range addition

**Key Learning:** Container management, STL algorithms for finding min/max, iterator ranges, exception handling, efficient operations on large datasets.

### Exercise 02: Mutated abomination

**Directory:** `ex02/`  
**Files to turn in:** `Makefile`, `main.cpp`, `MutantStack.{h,hpp}` and optional `MutantStack.tpp`

Create an iterable version of `std::stack` by implementing `MutantStack`.

**The problem:**
`std::stack` is the only STL container that is NOT iterable. This is a significant limitation.

**The solution:**
Create `MutantStack` class template that:
- Inherits from or contains `std::stack`
- Provides all standard stack operations
- **Adds iterator support** (begin(), end())

**Class template:**
```cpp
template<typename T>
class MutantStack : public std::stack<T> {
public:
    // Standard stack operations inherited
    // Add iterator support:
    typedef ??? iterator;
    iterator begin();
    iterator end();
};
```

**Requirements:**
- Must work exactly like `std::stack`
- Must be iterable with begin() and end()
- Should be compatible with standard algorithms
- Can be used to construct a `std::stack`

**Example usage:**
```cpp
MutantStack<int> mstack;
mstack.push(5);
mstack.push(17);

std::cout << mstack.top() << std::endl;
mstack.pop();
std::cout << mstack.size() << std::endl;

mstack.push(3);
mstack.push(5);
mstack.push(737);
mstack.push(0);

MutantStack<int>::iterator it = mstack.begin();
MutantStack<int>::iterator ite = mstack.end();

++it;
--it;
while (it != ite) {
    std::cout << *it << std::endl;
    ++it;
}

std::stack<int> s(mstack);  // Should work
```

**Testing requirement:**
Replace `MutantStack` with `std::list` and verify identical behavior (output should be the same).

**Key Learning:** Container adaptors, iterator implementation, inheritance with templates, understanding stack's underlying container, creating STL-compatible classes.

## Project Structure

```
CPP08/
├── ex00/
│   ├── Makefile
│   ├── main.cpp
│   ├── easyfind.hpp
│   └── easyfind.tpp (optional)
├── ex01/
│   ├── Makefile
│   ├── main.cpp
│   ├── Span.hpp
│   └── Span.cpp
├── ex02/
│   ├── Makefile
│   ├── main.cpp
│   ├── MutantStack.hpp
│   └── MutantStack.tpp (optional)
└── README.md
```

## Installation

1. **Clone the Repository:**

   ```sh
   git clone https://github.com/marco-ht/CPP08.git
   cd CPP08
   ```

2. **Build the Desired Exercise:**

   ```sh
   cd ex00 && make
   ```

## Usage

Each exercise produces its own executable. Navigate to the exercise directory and run:

**Exercise 00:**
```sh
./easyfind
```
Demonstrates finding values in various STL containers.

**Exercise 01:**
```sh
./span
```
Demonstrates the Span class with various operations and large datasets.

**Exercise 02:**
```sh
./mutantstack
```
Demonstrates the iterable MutantStack compared to standard containers.

## Submission and Peer Evaluation

- Submit your project through the designated Git repository.
- Only the files within your Git repository will be evaluated during defense.
- Double-check that all file names and structures match the subject requirements.
- Ensure your Makefile compiles without relinking and includes all required rules.
- **Critical:** Be prepared to justify your use of STL containers and algorithms during defense.
- Test extensively with various container types and edge cases.

## Acknowledgments

- Thanks to the 42 community, mentors, and fellow students for their guidance and support.
- Special thanks to resources on STL containers, iterators, and algorithms.
- The STL documentation at cplusplus.com and cppreference.com.

## Disclaimer

**IMPORTANT**:
This project was developed solely as part of the educational curriculum at 42 School. The code in this repository is published only for demonstration purposes to showcase my programming and C++ development skills.

**Academic Integrity Notice**:
It is strictly prohibited to copy or present this code as your own work in any academic submissions at 42 School. Any misuse or uncredited use of this project will be considered a violation of 42 School's academic policies.

## License

This repository is licensed under the Creative Commons - NonCommercial-NoDerivatives (CC BY-NC-ND 4.0) license. You are free to share this repository as long as you:

- Provide appropriate credit.
- Do not use it for commercial purposes.
- Do not modify, transform, or build upon the material.

For further details, please refer to the CC BY-NC-ND 4.0 license documentation.

Developed with dedication and in strict adherence to the high standards of 42 School.
