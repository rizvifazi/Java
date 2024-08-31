
---
## Question 01: Select the methods used to test for the equality of String values in Java.
- equalsIgnoreCase
- ==
- =
- ===
- test
- equals

### Answer:
- equalsIgnoreCase
- equals
- == -> Not recomended

#### Explanation:
- `equalsIgnoreCase`: Checks if two strings are equal, ignoring case considerations.
- `equals`: Checks if two strings are equal, considering case.
- `==`: Checks if two string references point to the same object in memory.

---


## Question 02: Match the integral primitive type with its size. (8/16/32/64)

### Answer Choices:
- A: long
- B: byte
- C: int
- D: short

### Answer:
- A: long - 64 bits
- B: byte - 8 bits
- C: int - 32 bits
- D: short - 16 bits

#### Explanation:
- `long` → 64 bits
- `byte` → 8 bits
- `int` → 32 bits
- `short` → 16 bits

---


## Question 03: Given the regular expression ‘\\s+’, which characters will be used for splitting words?
- spaces
- newlines
- tabs
- punctuation
- hyphens

### Answer:
- spaces
- newlines
- tabs

#### Explanation:
- `\\s+` matches any whitespace character, which includes spaces, newlines (`\n`), and tabs (`\t`).
- Punctuation and hyphens are not whitespace characters, so they are not matched by `\\s+`.

---


## Question 04: What does a negative return value indicate when calling the compareTo method on a String?
- An error has occurred when comparing the Strings
- The String is lexicographically less than the String argument
- The String is lexicographically greater than the String argument
- The String is equal to the String argument

### Answer:
- The String is lexicographically less than the String argument

#### Explanation:
- The `compareTo` method returns a negative value if the string is lexicographically less than the string argument, a positive value if greater, and zero if equal.

---


## Question 05: Match the feature description with its object type. (String/StringBuilder)

### Answer Choices:
- A: immutable
- B: methods for data manipulation: append, delete, insert, replace
- C: mutable
- D: instantiation without new

### Answer:
- String:
  - A: immutable
  - D: instantiation without new
- StringBuilder:
  - B: methods for data manipulation: append, delete, insert, replace
  - C: mutable

#### Explanation:
- **String** is immutable and can be instantiated without using `new`.
- **StringBuilder** is mutable and has methods like `append`, `delete`, `insert`, and `replace` for data manipulation.

---