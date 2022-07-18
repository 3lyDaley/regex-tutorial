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

`^` and `$`

Generally at the beginning and end of a string. For this example, we begin with `/^` and end with `$/` Where the forward slashes begin and end the statement. If the  `^` and `$` are both present, we are looking for an exact match of whatever is between them. 

### Quantifiers

`*`, `+`, `?`, and `{}`

Quantifiers communicate that the input must match the character or expression (char/ex), to it's immediate left, and must be present to a specific quantity depending on how they are explained in the statement.

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

`|` or `[]`

Using these operators communicates that you would like to find **either** one **or** the other. Within parentheses, using `|`, means that the char/ex will be captured. **Capturing** means that the multiple characters will be treated as a single unit. When the `[]` are used, the characters inside the brackets will not be captured as a single unit. 

Descriptions:
- `a(b|c)`: Matches a string, 'a' followed by either 'b' or 'c'. Captures 'b' or 'c'
- `a[bc]`: Same as above, but does not capture 'b' or 'c' 

Examples: 
- `[\da-z\.-]`: `\d`, `a-z`, `\.`, or `-` must appear after the char/ex they immediately follow in the Regex individually
- `[a-z\.]`: Same as above with letters `a-z` or a dot `\.`.
- `[\/\w \.-]`: Same as first example with `/`, a word character (`\w`), a dot `\.`, or a hyphen `-`.

### Character Classes

The `\d` and `\w` character classes have been explained above, and they represent a single character that is a **digit** and a **word character**, or alphanumeric character plus underscore, respectively. A period without a backslash, or just `.` rather than `\.` would match ***any*** character. This is why, in previous examples, a '.' is denoted as `\.`, as the backslash is used to escape the following character's default meaning.


### Flags

We see that our regex is placed within two forward slashes. This is how the search pattern of the regex is delimited. There are symbols that can be placed near these flags that will specify their values. 

- `g`: (global) does not return after the first match, restarting the subsequent searches from the end of the previous match
- `m`: (multi-line), When 'm' is enabled the `^` and `$` will match the start and end of one line rather than the whole string. 
- `i`: (insensitive) But will make the whole expression case-sensitive
- 
### Grouping and Capturing

Refer to [OR Operator](#or-operator) for a brief decsription of capturing. Grouping allows us to maintain a readable organization to our redex statement. `()` Indicate that all characters or symbols enclosed can appear at that specific place in the string. This is useful when dealing with varying syntax in different coding languages, or in our case, the variance of digits, characters, and symbols typical of URLs. 
<br>
Example: 
<br>
A URL is generally in the format of '`https://www.somewebsitehere.com/someidcontaining23213or!@#^%/`'.<br>
The structure of our redex allows each individual portion to contain any and all possible characters in the standard order of a URL. <br>

`(https?:\/\/)` followed by `([\da-z\.-]+)` followed by `.([a-z\.]{2,6})` and ending with `([\/\w \.-]*)` and a possible forward slash `*\/?`. 

### Bracket Expressions

Brackets provide similar benefits as parenthesis but are associated with **or**. A `([])` structure reads as 'and/or'. If an `^` is located within a bracket, it **negates** the contents of the bracket. There are no instances of that in our regex but an example is: <br>
`[^a-zA-Z] = a string that has NOT a letter from a-z OR A-Z`

### Greedy and Lazy Match

The quantifiers `*` and `{}` are greedy quantifiers. **Greedy** means that the quantifiers represent any amount of matches, or 1 > matches. I think this is best described in comparison to the **lazy** `?` quantifier, which means only 0-1 matches. 

### Boundaries

`\b` and `\B`

`\b`: Similar to the `^` and `$` anchors, but matches positions where one side is a word character, and the other side is not. (this could be the beginning of the string or whitespace).

Capital `\B` is the **negation**, which means the pattern **must be surrounded** by word characters.

### Back-references

Backreferences match the same text as previously matched by a capturing group. This explanation feels a bit maze-y so I'll use an example.

If you were denoting HTML with the same opening/closing tags, such as a `<div>`, you can simplify your redex by writing:<br>
 `<([a-z]+)([^<]+)*(?:>(.*)<\/\1>` rather than `<([a-z]+)([^<]+)*(?:>(.*)<\/([a-z]+)([^<]+)*(?:>`. <br>
 The `\1` references what is in the first set of parentheses when reading the line from left to right. It starts reading at the opening parentheses, and ends at the closing. Whenever it is backreferenced by `\1`, that is the value of the reference.
 
### Look-ahead and Look-behind

`(?=)` and `(?<=)`

Example: 
- `d(?=r)`: Matches **only** if 'd' is *followed by* 'r', but 'r' will not be included in the regex match.
- `(?<=r)d`: Matches **only** if 'd' is **NOT** *preceded by* an 'r', but 'r' will not be included in the regex match.

## Author

Thanks for reading! The author of this tutorial is Ely Daley, who can be found and contacted through their [Github](https://github.com/3lyDaley).
