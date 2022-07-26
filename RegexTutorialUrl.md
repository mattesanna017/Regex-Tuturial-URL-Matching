# Regex-Tutorial-URL-Matching

We will look at a regular expression for matching a URL in this tutorial. With the help of this illustration, we can start to develop a fundamental grasp of regular expressions, including what each component signifies, how to use them in code to specify search patterns, and how to verify that particular strings satisfy particular requirements. This guide is only meant to serve as a very basic introduction to regular expressions; it does not attempt to cover all of their complexity.

## Summary
The following regular expression can be used, as was already said, to verify that a string is, in fact, a URL.
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```
To explain it plainly, this expression can be summarised as follows:
- Start the string with `https:// `
- The string can then contain any value between `0 and 9`, along with any lowercase letter between `a and z`,`.`, `or` -. This pattern might be repeated one or more times throughout the string.
- `.` must adhere to the prior pattern
- The following portion of the string needs to contain any lowercase letters `(a-z)`,., and be between `2 and 6` characters long.
- The next characters in the string may be `any alphanumeric character` from the Latin alphabet, including `_`,`.`, or `-`. This pattern may occur once or more.
- The previous pattern can be followed by `/ 0` or one time

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components
Regular expressions are constructed from numerous distinct parts. It's critical to keep in mind that these expressions must be enclosed in slash letters / because regex is seen as a literal. We can see `/` at the start and end of our sample expression for matching a URL.

```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

We will now examine each part of this statement that makes it up.

### Anchors

The two anchor characters used in regex are `^` and `$` 

This anchor `^` marks the start of the string that should come after the expression at the beginning. There are two methods to use this anchor:

- to denote a perfect match, such as `^ABC.` Also both `"ABC"` and `"ABCDEFG"` would match.
- to use bracket expressions to represent a range of potential matches. Bracket expressions will be covered in a subsequent section.

### Quantifiers
Quantifiers in regex specify how many characters or expressions must match. We will examine each kind of quantifier first, and then we will examine the particular quantifiers used in our regex example for matching a URL.

- `*` - Does not match the previous pattern 0 or more times. For instance, `/fun*/` matches `"fun"` in `"funny"` and `"un"` in `"thunder"`, but `"bird"` is unmatched.

- `+` - At least one match is made to the previous pattern. For instance, `"kick"` matches each `k` using `/k+/`.

- 0 or 1 occurrences of the previous pattern are matching. Example: `/e?el?/` corresponds to the letters `"el"` in `"gel"` and `"le"` in `"cradle"`. An important thing to remember about the quantifier `?` is that it makes the quantifier non-greedy, which means it will match the minimum number of times instead of the default, which matches the maximum number of times, if it is used immediately after another quantifier `(*, +,?, or {})`.

- `{n, x}` - Matches the previous pattern at least `n` times and up to `x` times.

If we go back to our URL matching regex example, we can look at the various quantifiers that are used in the expression.
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```
- We can see `?` utilised in several number of locations. First, to indicate that `"https"` may match 0 or 1 times, followed by `"https//"` and finally, at the end, to indicate that `"/"` may match 0 or 1 times.

- We observe that the symbol `*` is used to indicate that `[\/\w \.-]` may match 0 or more times, as well as that `([a-z\.]{2,6})([\/\w \.-]*)` may match 0 or more times.
### Grouping Constructs
Regex uses grouping constructs to examine various pieces or sections of a string for compliance with various specifications. We can generate subexpressions with distinct criteria by enclosing various parts of the regex in parentheses `(())`.

In the absence of explicit instructions, Subexpressions search for exact matches. For instance, `"abc:def"` would fit the subexpression `(abc):(def)`, although `"cba:fed"` would not.

In the regex example we used to match a URL:
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```
the following subexpressions are present:
- `(https?:\/\/)`
- `([\da-z\.-]+)`
- `([a-z\.]{2,6})`
- `([\/\w \.-]*)`

### Bracket Expressions
Positive Character Groups, sometimes referred to as Bracket Expressions, represent a range of characters that we want to match in our string. Although we can write Bracket Expressions with any character we like, it is more typical to use a hyphen to denote a range of these characters. For instance, `[abcdef]` and `[a-f]` both suggest that we are looking for a string that contains the letters `a`, `b`, `c`, `d`, `e`, or `f`. It will be regarded as a match if the string contains at least one of the given characters.

As an example of a regex that matches a URL:
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```
The following bracket expressions are visible:
- Any numerical digit, any lowercase letter (a-z), a slash, a dot, or a hyphen will result in a match with the bracket expression `[\da-z\.-]` . 
- Any lowercase letter, slash, or dot, as well as the bracket phrase `[a-z\.]` will result in a match.
- Any slash, any alphanumeric character, a dot, or a hyphen will result in a match when entered in the brackets `[\/\w \.-]`.

### Character Classes
Regex uses character classes to specify groups of characters from which a match can be made in a string. One common kind of character is the Bracket Expression, which was covered in the preceding section. Here are a few additional typical character classifications.

- `.` - Except for `/n` (new line), it matches any character 
- `/d` - it matches any numerical digit
- `/w`- it matches any latin alphabet alphanumeric character, including an underscore (`_`).
- `/` - it matches a single character of whitespace, such as tabs and line breaks.

In the regex example we used to match a URL:
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```
using character classes, we observe the following:
- `[\da-z\.-]`-we can see that the character class `/d` is being used to denote that any number digit will result in a match within this bracket expression.
- `[\/\w \.-]` -we can see that the symbol /w, which denotes that any alphanumeric character from the latin alphabet will result in a match, is utilised within this bracket expression.

### The OR Operator
In this regex:
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```
`[]` serves as the primary OR operator. All characters or character classes that are enclosed in brackets will match the expression. As an illustration, the `[\da-z\.-]` expression matches for any digits (`/d`) OR any characters in the range of a to z (`a-z`) OR any '.' (`\.`) OR any '-' (`-`).


### Flags
While learning how to build regexes, we are overlooking a crucial idea: flags.

The most common format for a regex is `/abc/`, where the search pattern is separated by two slash characters `/`. We can specify a flag at the conclusion with the following values (or a combination of them):
- The subsequent searches are restarted from the conclusion of the initial match when 'g' (global) does not return following the first match.
- When 'm' (multi-line) is enabled, `^` and `$` will only match the beginning and end of a line rather than the entire string.
- The letter 'i' (insensitive) makes the entire expression case-insensitive (for example, `/aBc/i` would match `AbC`).

### Character Escapes
Regex notates Character Escapes with a backslash (`\`). When a character is not intended to be taken literally, character escapes are employed. For instance, the character typically denotes the start of a quantifier, but if we use the backslash character (`\{`) before the curly brace, regex will search for an opening curly brace rather than the start of a quantifier. When looking for strings with special characters, this can be helpful. Character escapes and all other special characters have the drawback of becoming useless when used inside bracket expressions.

Analyzing our regex example for URL matching:
```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```
We can see instances in which a character escape is used.
- `\.` - here, it's used to show that the character is what we're seeking for `.` specifically, rather than the character class

## Author
The author of this Regex Tutorial is Matteo Sanna. 

In 2022, Matteo attended University of Manchester Coding Bootcamp to study web development. He likes working on new projects and participating in the developer community. You may check out more of his work by going to his [Github Profile](https://github.com/mattesanna017).