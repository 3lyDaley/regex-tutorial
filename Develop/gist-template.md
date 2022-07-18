# Regex tutorial: Matching a URL  


## Summary

A tutorial on the regex expression that checks and matches a URL:

```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

```^``` AND ```$```
Generally at the beginning and end of a string. For this example, we begin with ```/^``` and end with ```$/``` Where the forward slashes begin and end the statement. If the  ```^``` and ```$``` are both present, we are looking for an exact match of whatever is between them. Otherwise, the ```^``` would be looking for a match of whatever character, or group, was to its right, and ```$``` would be looking for an exact match to the character or group to its left.  

### Quantifiers

`*`, `+`, `?`, and `{}`

Quantifiers communicate that the input must match the character or expression (char/ex), to it's immediate left must be present to a specific quantity depending on how they are grouped in the statement.

Descriptions:

- `*` Means that the char/ex to the left of the asterisk must appear 0 or more after the char/ex to the left of it. 
- `+` The char/ex left of the plus sign must appear once or more after the char/ex to the left of it.
- `?` The char/ex left of the question mark must appear 0 or 1 time after the char/ex to the left of it.
- `https{2}` Requires a string, 'http' to be followed by exactly 2 's'
- `https{2, 10}` Requires 'http' must be followed by at least two and up to ten 's'.  

Examples:
- `https?`: There must be 0-1 's' following 'http'
- `[\da-z\.-]+`: Within the square brackets, there is a single digit (`\d`), group of letters (`a-z`), a dot (`\.`), and/or a hyphen (`-`). The `+` indicates that there must be one or more of these characters following the previous char/ex.
- `([a-z\.]{2,6})`: There must be 2-6 instances of the (`a-z`) or `-` characters following the previous expression.
- `[\/\w \.-]*`: There must be 0-1 instances of a word character (alphanumberic character plus an underscore) indicated by `\w`, and/or 0-1 instances of `/`, and/or `.`.
- `)*`: 0-1 closing parentheses after the previous char/ex



### OR Operator

### Character Classes

### Flags

### Grouping and Capturing

### Bracket Expressions

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
