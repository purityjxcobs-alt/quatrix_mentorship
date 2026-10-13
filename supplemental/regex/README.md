# RegEx Metacharacters & Literals
## Short Notes 

# Module: RegEx Metacharacters & Literals

*   **Literals (e.g., `buzz123`)**: Matches the exact sequence of alphanumeric characters as they are.
*   **`.` (Dot)**: Matches any single character (letters, numbers, or special characters).
*   **`^` (Caret)**: Matches the **beginning** of a line. *(Note: Negates characters if used inside square brackets).*
*   **`$` (Dollar)**: Matches the **end** of a line.
*   **`?` (Question Mark)**: Indicates a **non-greedy** match for the preceding pattern.
*   **`*` (Asterisk)**: Matches **0 or more** occurrences of the preceding element (e.g., `.*` matches any character 0+ times; `f*` matches "f" 0+ times).
*   **`+` (Plus)**: Matches **1 or more** occurrences of the preceding element (e.g., `.+` matches any character 1+ times; `f+` matches "f" 1+ times).
*   **`|` (Vertical Bar)**: Acts as an **OR** condition (e.g., `a|b` matches "a" or "b"). Do not confuse this with a command-line pipe.
*   **`[]` (Square Brackets)**: Matches any single character within the set (e.g., `[abc]` matches "a", "b", or "c"). Using a caret inside negates it (e.g., `[^abc]` matches any character *except* "a", "b", or "c").
*   **`{}` (Curly Brackets)**: Specifies exact **quantities** to match:
    *   `z{1}`: Exactly 1 occurrence of "z".
    *   `z{1,}`: 1 or more occurrences of "z".
    *   `z{2,}`: 2 or more occurrences of "z".
    *   `z{2,4}`: Between 2 and 4 occurrences of "z".
*   **`()` (Parentheses)**: Defines **capture groups** used to save matched patterns for search-and-replace actions (e.g., `(Ken)ya` captures "Ken"). 
*   **`\` (Backslash)**: The **escape character**. It turns a metacharacter into a literal character (e.g., `\.` matches a literal period; `\?` matches a literal question mark).



# Question 1

## Find all prices formatted with a dollar sign followed by numbers, a decimal point, and exactly two cents digits (e.g., $4.99, $125.50).

    \$\d+\.\d*

# Question 2

## Finding Exact NumbersTask: Highlight every 4-digit product code (e.g., 1024, 9890), while ignoring 3-digit IDs or 5-digit order numbers.

    \s\d{4}\s

# Question 3 

## Find all phone numbers starting with 555 followed by four digits, whether there is a hyphen - between them or not (matching both 555-0199 and 5550199).

    555(-|:|)\d{4}

# Question 4 

## Write a single pattern to find both American and British spellings of gray and grey.

    gr(e|a)y

# Question 5 

## Find all log entries that occurred in the year 2026 formatted as 2026-MM-DD (e.g., 2026-09-30), ignoring entries from other years

    \s\d{4}(-)\d*(-)\d*

# Question 6 

## Match any opening or closing HTML tag in the document (e.g., <b>, </i>, <h1>, </div>).

    <(/|)\w+(>|)

# Question 7 

## In the Replace tool, convert names formatted as Firstname Lastname (e.g., Alice Smith) into Lastname, Firstname (e.g., Smith, Alice).

 Find (\w+)\s(\w+)


 Replace \2, \1

# Question 8 

## In the Replace tool, convert dates written in DD/MM/YYYY format (e.g., 30/09/2026) to ISO format YYYY-MM-DD (e.g., 2026-09-30).

 Find (\d{2})/(\d{2})/(\d{4})

 Replace \3-\2-\1

# Question 9 

## In the Replace tool, find all occurrences of two or more consecutive spaces between words and replace them with a single space.

    Find \s{1,}

    Replace space or " "

# Question 10 

## Find only the lines that start with the word IMPORTANT at the very beginning of the line, ignoring lines where IMPORTANT is indented with spaces or tabs.

 Find ^important.*$


## Table of Contents

1. [What is Regex?](#1-what-is-regex)
2. [Where Regex is Used](#2-where-regex-is-used)
3. [Regex Flavors](#3-regex-flavors)
4. [Literal Characters](#4-literal-characters)
5. [Metacharacters Overview](#5-metacharacters-overview)
6. [Character Classes](#6-character-classes)
7. [Anchors](#7-anchors)
8. [Quantifiers](#8-quantifiers)
9. [Groups & Capturing](#9-groups--capturing)
10. [Alternation](#10-alternation)
11. [Special Escapes](#11-special-escapes)
12. [Lookarounds (Lookahead & Lookbehind)](#12-lookarounds-lookahead--lookbehind)
13. [Backreferences](#13-backreferences)
14. [Flags / Modifiers](#14-flags--modifiers)
15. [Greedy vs Lazy Matching](#15-greedy-vs-lazy-matching)
16. [Regex in Bash (grep, sed, awk)](#16-regex-in-bash-grep-sed-awk)
17. [Regex in Programming Languages](#17-regex-in-programming-languages)
18. [Common Regex Patterns (Cheat Sheet)](#18-common-regex-patterns-cheat-sheet)
19. [Regex Testing & Debugging](#19-regex-testing--debugging)
20. [Practice Questions & Answers](#20-practice-questions--answers)
21. [Exam-Style Questions](#21-exam-style-questions)
22. [Quick Reference Cheat Sheet](#22-quick-reference-cheat-sheet)

---

## 1. What is Regex?

A **Regular Expression** (regex or regexp) is a sequence of characters that defines a **search pattern**. It is used to match, search, replace, and validate text.

### Detailed Explanation

Regex is essentially a mini-language for describing patterns in strings. Instead of searching for exact literal text ("hello"), you can search for abstract patterns like:
- "Any 3-digit number" → `\d{3}`
- "Any email address" → `\S+@\S+\.\S+`
- "Lines that start with 'Error'" → `^Error`

**Key characteristics:**
- **Declarative:** You describe what you want, not how to find it.
- **Concise:** A tiny pattern can describe a complex search.
- **Portable:** Supported in most languages and tools (with minor differences).
- **Powerful but tricky:** Easy to get wrong; always test.

**Q: What is a regular expression?**
**A:** A sequence of characters defining a search pattern, used for matching, searching, replacing, and validating text.

**Q: Why use regex?**
**A:** To find patterns (not just literal strings), validate input (emails, phone numbers), extract data (log parsing), and replace text dynamically.

---

## 2. Where Regex is Used

Regex shows up almost everywhere in computing:

| Domain | Use Case |
|--------|----------|
| **Text editors** | Search and replace in VS Code, Vim, Sublime |
| **Command line** | `grep`, `sed`, `awk`, `ripgrep` |
| **Programming** | Python (`re`), JavaScript (`RegExp`), Java, PHP, Ruby, Go |
| **Web forms** | Input validation (email, phone, password strength) |
| **Log analysis** | Finding errors, extracting IPs, parsing timestamps |
| **Data cleaning** | Removing whitespace, standardizing formats |
| **URL routing** | Matching routes like `/users/:id` |
| **Compilers/Lexers** | Tokenizing source code |
| **Databases** | `REGEXP` in MySQL, `~` in PostgreSQL |

**Q: Name three tools that use regex.**
**A:** `grep`, `sed`, and `awk` (also Python, JavaScript, Vim, etc.).

**Q: What's a real-world use case for regex?**
**A:** Validating email addresses in a sign-up form, or extracting error messages from a log file.

---

## 3. Regex Flavors

Not all regex is the same. Different tools implement different "flavors":

| Flavor | Used By | Notes |
|--------|---------|-------|
| **POSIX Basic (BRE)** | `grep`, `sed` (default) | Metacharacters like `+`, `?`, `{}` must be escaped |
| **POSIX Extended (ERE)** | `grep -E`, `egrep`, `awk` | `+`, `?`, `{}`, `()` work directly |
| **PCRE** | Perl, PHP, Python (`re`) | Richest feature set (lookarounds, backreferences) |
| **JavaScript** | Node.js, browsers | Similar to PCRE, slight differences |
| **.NET** | C#, PowerShell | Very rich, includes named groups |
| **RE2** | Go, Google tools | Fast, but no backreferences or lookarounds |

**Important for exams:** What works in `grep` (BRE) may need escaping in `grep -E` (ERE), and vice versa.

**Q: What is the difference between BRE and ERE?**
**A:** In BRE (Basic Regular Expressions), metacharacters like `+`, `?`, `{`, `}`, `(`, `)` must be escaped with `\` to get their special meaning. In ERE (Extended), they work directly.

**Q: What is PCRE?**
**A:** Perl Compatible Regular Expressions — the most feature-rich flavor, used by Perl, PHP, Python (`re`), and others.

---

## 4. Literal Characters

Any character that isn't a metacharacter matches itself.

```
abc      → matches "abc"
hello    → matches "hello"
123      → matches "123"
```

**Case sensitivity:** By default, regex is case-sensitive. `abc` does NOT match `ABC`. Use flags to change this.

**Q: Does `abc` match `ABC`?**
**A:** No, by default. Add the `i` flag (case-insensitive) to allow it.

**Q: Does `a.b` match `a.b`?**
**A:** Not exactly — the `.` is a metacharacter matching any character. To match a literal dot, escape it: `a\.b`.

---

## 5. Metacharacters Overview

Metacharacters have special meaning in regex. To match them literally, escape with `\`.

| Metacharacter | Meaning |
|---------------|---------|
| `.` | Any single character (except newline by default) |
| `^` | Start of line/string |
| `$` | End of line/string |
| `*` | Zero or more of the previous |
| `+` | One or more of the previous |
| `?` | Zero or one of the previous (optional) |
| `\|` | Alternation (OR) |
| `()` | Grouping / capturing |
| `[]` | Character class |
| `{}` | Quantifier (exact count or range) |
| `\` | Escape character |

**Q: How do you match a literal dot?**
**A:** Escape it: `\.`

**Q: How do you match a literal `$`?**
**A:** Escape it: `\$`

**Q: What does `.` match?**
**A:** Any single character except newline (unless the `s` flag is set, which makes it match newlines too).

---

## 6. Character Classes

A **character class** `[...]` matches **any one** of the characters inside.

### Basic Classes

```
[abc]        → matches a, b, or c
[xyz]        → matches x, y, or z
[0-9]        → matches any digit
[a-z]        → matches any lowercase letter
[A-Z]        → matches any uppercase letter
[a-zA-Z]     → matches any letter (upper or lower)
[a-zA-Z0-9]  → matches any letter or digit
[^abc]       → matches any character EXCEPT a, b, or c (negated class)
```

### Important Rules

- Inside `[]`, most metacharacters lose their special meaning.
  - `[.]` matches a literal dot (no need to escape).
  - `[*]` matches a literal asterisk.
- To include a literal `]`, place it first: `[]abc]`.
- To include a literal `-`, place it first or last: `[-abc]` or `[abc-]`.
- To include `^`, don't put it first: `[a^b]`.

### Predefined Classes (Shorthand)

| Shorthand | Meaning | Equivalent |
|-----------|---------|------------|
| `\d` | Any digit | `[0-9]` |
| `\D` | Any non-digit | `[^0-9]` |
| `\w` | Any word character | `[a-zA-Z0-9_]` |
| `\W` | Any non-word character | `[^a-zA-Z0-9_]` |
| `\s` | Any whitespace | `[ \t\n\r\f\v]` |
| `\S` | Any non-whitespace | `[^ \t\n\r\f\v]` |

### POSIX Classes

| POSIX | Meaning |
|-------|---------|
| `[:alpha:]` | Letters |
| `[:digit:]` | Digits |
| `[:alnum:]` | Letters and digits |
| `[:space:]` | Whitespace |
| `[:upper:]` | Uppercase letters |
| `[:lower:]` | Lowercase letters |
| `[:punct:]` | Punctuation |

Example: `[[:digit:]]` matches a digit in POSIX.

**Q: What does `[^abc]` match?**
**A:** Any single character that is NOT a, b, or c.

**Q: What is the shorthand for "any digit"?**
**A:** `\d` (in PCRE) or `[0-9]` (universal).

**Q: What is the difference between `\w` and `\W`?**
**A:** `\w` matches word characters (letters, digits, underscore); `\W` matches anything that is NOT a word character.

---

## 7. Anchors

**Anchors** don't match characters — they match **positions** in the string.

| Anchor | Meaning |
|--------|---------|
| `^` | Start of line (or string) |
| `$` | End of line (or string) |
| `\b` | Word boundary |
| `\B` | Non-word boundary |
| `\A` | Start of string (PCRE) |
| `\Z` | End of string (PCRE) |
| `\z` | Absolute end of string (PCRE) |

### Examples

```
^Hello          → matches "Hello" only at the start of a line
World$          → matches "World" only at the end of a line
^Hello World$   → matches the entire line exactly
\bcat\b         → matches "cat" as a whole word (not "catch")
\Bcat           → matches "cat" only if preceded by a word character
```

**Q: Difference between `^` and `\A`?**
**A:** `^` matches the start of a **line** (or string in multiline mode); `\A` matches the start of the **entire string**, regardless of mode.

**Q: What does `\b` do?**
**A:** Matches a word boundary — the position between a word character and a non-word character.

**Q: Why does `^` behave differently across tools?**
**A:** In multiline mode, `^` matches at the start of every line, not just the whole string.

---

## 8. Quantifiers

**Quantifiers** specify how many times the previous character/group should be matched.

| Quantifier | Meaning |
|------------|---------|
| `*` | 0 or more |
| `+` | 1 or more |
| `?` | 0 or 1 (optional) |
| `{n}` | Exactly n times |
| `{n,}` | n or more |
| `{n,m}` | Between n and m (inclusive) |

### Examples

```
a*        → matches "", "a", "aa", "aaa"
a+        → matches "a", "aa", "aaa" (but not "")
a?        → matches "" or "a"
a{3}      → matches "aaa" only
a{2,5}    → matches "aa", "aaa", "aaaa", "aaaaa"
a{3,}     → matches "aaa", "aaaa", "aaaaa", ...
[0-9]{4}  → matches exactly 4 digits
```

**Q: Difference between `*` and `+`?**
**A:** `*` matches zero or more; `+` matches one or more.

**Q: What does `a?` match?**
**A:** Either zero or one "a" (i.e., the "a" is optional).

**Q: What does `[0-9]{2,4}` match?**
**A:** Between 2 and 4 digits (inclusive).

---

## 9. Groups & Capturing

**Parentheses `()`** create a group. Groups serve two purposes:
1. **Grouping:** Apply quantifiers or alternation to a sub-pattern.
2. **Capturing:** Save the matched text for later use (backreferences or programmatic access).

### Examples

```
(abc)+           → matches "abc", "abcabc", "abcabcabc"
(ab|cd)          → matches "ab" or "cd"
(\d{3})-(\d{4})  → captures two groups: area code and number
```

### Capturing Groups

In most languages, you can access captured groups:

```python
import re
m = re.search(r'(\d{3})-(\d{4})', '555-1234')
m.group(1)  # '555'
m.group(2)  # '1234'
```

### Non-Capturing Groups

`(?:...)` groups without capturing — useful when you just want to apply a quantifier:

```
(?:abc)+   → matches "abcabc" but doesn't save the match
```

### Named Groups

Some flavors (PCRE, Python) allow named groups:

```
(?P<area>\d{3})-(?P<number>\d{4})
```

**Q: What's the difference between a capturing and non-capturing group?**
**A:** Capturing groups `()` save the matched text; non-capturing groups `(?:...)` group without saving.

**Q: Why use non-capturing groups?**
**A:** They improve readability and performance when you only need to apply a quantifier or alternation without saving the match.

---

## 10. Alternation

**Alternation** uses `|` to match one of several options.

```
cat|dog          → matches "cat" or "dog"
yes|no|maybe     → matches "yes", "no", or "maybe"
(abc|def)ghi     → matches "abcghi" or "defghi"
```

**Important:** Without parentheses, `|` has the lowest precedence:

```
^cat|dog$        → matches "^cat" OR "dog$" (not what you probably want)
^(cat|dog)$      → matches a line that is exactly "cat" or "dog"
```

**Q: What does `cat|dog` match?**
**A:** Either the string "cat" or the string "dog".

**Q: Why do you often need parentheses around alternations?**
**A:** To limit the scope of `|`, since it has the lowest precedence. `^(cat|dog)$` restricts the alternation to the group.

---

## 11. Special Escapes

Some characters have special meaning; to match them literally, escape with `\`:

| Literal Character | Regex Escape |
|-------------------|--------------|
| `.` | `\.` |
| `*` | `\*` |
| `+` | `\+` |
| `?` | `\?` |
| `(` | `\(` |
| `)` | `\)` |
| `[` | `\[` |
| `]` | `\]` |
| `{` | `\{` |
| `}` | `\}` |
| `\|` | `\\|` |
| `^` | `\^` |
| `$` | `\$` |
| `\` | `\\` |

### Other Escapes

| Escape | Meaning |
|--------|---------|
| `\n` | Newline |
| `\t` | Tab |
| `\r` | Carriage return |
| `\f` | Form feed |
| `\v` | Vertical tab |
| `\0` | Null character |
| `\xHH` | Character with hex code HH |
| `\uHHHH` | Unicode character |

**Q: How do you match a literal `+`?**
**A:** `\+`

**Q: What does `\n` match?**
**A:** A newline character.

---

## 12. Lookarounds (Lookahead & Lookbehind)

**Lookarounds** check for a pattern without consuming characters (zero-width assertions).

### Types

| Syntax | Name | Meaning |
|--------|------|---------|
| `(?=...)` | Positive lookahead | Followed by `...` |
| `(?!...)` | Negative lookahead | NOT followed by `...` |
| `(?<=...)` | Positive lookbehind | Preceded by `...` |
| `(?<!...)` | Negative lookbehind | NOT preceded by `...` |

### Examples

```
\d+(?= dollars)         → matches digits followed by " dollars" (without consuming " dollars")
\d+(?! dollars)         → matches digits NOT followed by " dollars"
(?<=\$)\d+              → matches digits preceded by "$" (without consuming "$")
(?<!\$)\d+              → matches digits NOT preceded by "$"
```

### Real-world Use

**Password with at least one digit:**
```
^(?=.*\d).{8,}$
```
(At least 8 characters, contains a digit.)

**Q: What is a lookahead?**
**A:** A zero-width assertion that checks whether a pattern appears ahead, without consuming characters.

**Q: What is the difference between `(?=...)` and `(?!...)`?**
**A:** `(?=...)` requires the pattern to be present; `(?!...)` requires it to NOT be present.

**Q: Why are lookarounds useful?**
**A:** They let you match based on surrounding context without including that context in the match.

---

## 13. Backreferences

A **backreference** matches the same text that was previously captured by a group.

```
(\w+)\s+\1      → matches a repeated word (e.g., "hello hello")
(abc)\1         → matches "abcabc"
(['"]).*?\1     → matches text inside matching quotes
```

`\1` refers to the first captured group, `\2` to the second, etc.

**Q: What does `(\w+)\s+\1` match?**
**A:** A word followed by whitespace, followed by the SAME word. E.g., "hello hello", "test test".

**Q: Which regex flavors support backreferences?**
**A:** PCRE, Python, JavaScript, .NET. RE2 (used by Go and some Google tools) does NOT support backreferences.

---

## 14. Flags / Modifiers

**Flags** change how the regex engine interprets the pattern.

| Flag | Meaning |
|------|---------|
| `i` | Case-insensitive |
| `g` | Global (find all matches, not just first) |
| `m` | Multiline (`^` and `$` match at line breaks) |
| `s` | Dotall (`.` matches newline too) |
| `x` | Extended (ignore whitespace in pattern for readability) |
| `u` | Unicode mode |
| `U` | Ungreedy (swap greedy/lazy behavior) |

### Examples

```python
import re
re.findall(r'hello', 'HELLO hello Hello', re.IGNORECASE)   # ['HELLO', 'hello', 'Hello']
```

```javascript
"abc ABC".match(/abc/gi)   // ['abc', 'ABC']
```

**Q: What does the `i` flag do?**
**A:** Makes the pattern case-insensitive.

**Q: What does the `g` flag do in JavaScript?**
**A:** Finds all matches, not just the first one.

**Q: What does the `m` flag do?**
**A:** Makes `^` and `$` match at every line break, not just the start/end of the whole string.

---

## 15. Greedy vs Lazy Matching

By default, quantifiers are **greedy** — they match as much as possible.
Adding `?` after a quantifier makes it **lazy** — it matches as little as possible.

### Examples

For the string `<b>bold</b> <i>italic</i>`:

```
<.*>        → matches the whole string (greedy)
<.*?>       → matches "<b>" (lazy)
<.+>        → matches the whole string (greedy)
<.+?>       → matches "<b>" (lazy)
```

| Pattern | Type |
|---------|------|
| `*` | Greedy |
| `*?` | Lazy |
| `+` | Greedy |
| `+?` | Lazy |
| `?` | Greedy |
| `??` | Lazy |
| `{n,m}` | Greedy |
| `{n,m}?` | Lazy |

**Q: What is greedy matching?**
**A:** The regex engine tries to match as much as possible before backtracking.

**Q: How do you make a quantifier lazy?**
**A:** Add `?` after it: `*?`, `+?`, `??`, `{n,m}?`.

**Q: Which is faster?**
**A:** Lazy is not necessarily faster; performance depends on the pattern. Lazy usually matches less, but greedy can be more efficient in some cases due to fewer backtracking steps.

---

## 16. Regex in Bash (grep, sed, awk)

### grep

```bash
grep 'pattern' file.txt
grep -E 'pattern' file.txt       # Extended regex (ERE)
grep -P 'pattern' file.txt       # Perl-compatible regex (PCRE)
grep -i 'pattern' file.txt       # Case-insensitive
grep -v 'pattern' file.txt       # Invert
grep -o 'pattern' file.txt       # Only the matched part
grep -c 'pattern' file.txt       # Count matches
```

**Examples:**

```bash
grep -E '^[A-Z]' file.txt                 # Lines starting with a capital letter
grep -E '[0-9]{3}-[0-9]{4}' file.txt      # Phone numbers
grep -iE 'error|warning' log.txt          # Errors or warnings
grep -oP '\d+\.\d+\.\d+\.\d+' log.txt     # IP addresses
```

### sed

```bash
sed 's/pattern/replacement/' file.txt         # Replace first per line
sed 's/pattern/replacement/g' file.txt        # Replace all
sed -E 's/[0-9]+/NUM/g' file.txt              # Extended regex
sed -n '/pattern/p' file.txt                  # Print matching lines
```

### awk

```bash
awk '/pattern/' file.txt                      # Print matching lines
awk '$1 ~ /^[0-9]+$/' file.txt                # Lines where field 1 is a number
```

**Q: Why does `grep -E` matter?**
**A:** In default `grep` (BRE), special characters like `+`, `?`, `{}`, `()` must be escaped. In `grep -E`, they work directly.

**Q: How do you use regex in sed to replace all digits with "X"?**
**A:** `sed -E 's/[0-9]+/X/g' file.txt`

---

## 17. Regex in Programming Languages

### Python (`re` module)

```python
import re

re.search(r'\d+', 'abc123')     # Match object for '123'
re.match(r'\d+', '123abc')      # Match at start
re.findall(r'\d+', 'a1b2c3')    # ['1', '2', '3']
re.sub(r'\d+', 'X', 'a1b2')     # 'aXbX'
re.split(r',\s*', 'a, b,c')     # ['a', 'b', 'c']
```

- Use **raw strings** `r'...'` to avoid escaping issues.

### JavaScript

```javascript
/pattern/flags                    // Literal regex
new RegExp('pattern', 'flags')    // Constructor
'abc123'.match(/\d+/)             // ['123']
'abc123'.replace(/\d+/, 'X')      // 'abcX'
/\d+/.test('abc123')              // true
```

### Java

```java
Pattern p = Pattern.compile("\\d+");
Matcher m = p.matcher("abc123");
m.find();                         // true
```

Note: In Java, you escape with `\\` because `\` is also the string escape character.

**Q: What prefix should you use in Python for regex strings?**
**A:** `r` (raw string) — `r'\d+'` instead of `'\\d+'`.

---

## 18. Common Regex Patterns (Cheat Sheet)

| Purpose | Pattern |
|---------|---------|
| Email | `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}` |
| Phone (US) | `\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}` |
| URL | `https?://[^\s]+` |
| IPv4 | `\b(?:\d{1,3}\.){3}\d{1,3}\b` |
| Date (YYYY-MM-DD) | `\d{4}-\d{2}-\d{2}` |
| Time (HH:MM) | `\d{2}:\d{2}` |
| Hex color | `#(?:[0-9a-fA-F]{3}){1,2}` |
| ZIP code (US) | `\d{5}(-\d{4})?` |
| Username | `^[a-zA-Z0-9_]{3,16}$` |
| Strong password | `^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$` |
| Whitespace | `\s+` |
| Trailing whitespace | `\s+$` |
| Empty lines | `^\s*$` |
| Numbers only | `^\d+$` |
| Letters only | `^[A-Za-z]+$` |
| Alphanumeric | `^[A-Za-z0-9]+$` |
| HTML tag | `<([a-z]+)([^>]*)>(.*?)</\1>` |
| Markdown link | `\[([^\]]+)\]\(([^)]+)\)` |
| Repeated word | `\b(\w+)\s+\1\b` |

**Q: What pattern matches an email?**
**A:** `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}`

**Q: What pattern matches a date in YYYY-MM-DD?**
**A:** `\d{4}-\d{2}-\d{2}`

---

## 19. Regex Testing & Debugging

Regex is notoriously tricky. Always test your patterns before deploying.

### Tools

| Tool | URL / Command |
|------|---------------|
| regex101 | https://regex101.com |
| regexr | https://regexr.com |
| Online regex testers | various |
| `grep --color=always` | Terminal testing |
| Python REPL | `python3 -c "import re; ..."` |

### Tips

1. **Start simple.** Build up patterns piece by piece.
2. **Test edge cases.** Empty strings, very long strings, special characters.
3. **Watch for catastrophic backtracking.** Nested quantifiers like `(a+)+` can explode.
4. **Use anchors** (`^`, `$`) to avoid partial matches.
5. **Escape special characters** when in doubt.
6. **Use raw strings in Python** (`r'...'`).
7. **Read the docs for your flavor** (Python vs JavaScript vs PCRE may differ).

**Q: What is catastrophic backtracking?**
**A:** A performance issue where a regex tries an exponential number of paths to find a match, often due to nested quantifiers.

**Q: Why test regex before using it in production?**
**A:** Regex can silently fail, match too much, or match too little. Testing ensures it behaves as expected.

---

## 20. Practice Questions & Answers

### Section A: Basics

**Q1.** What is a regular expression?
**A:** A sequence of characters defining a search pattern.

**Q2.** What does `.` match?
**A:** Any single character except newline.

**Q3.** What does `*` mean?
**A:** Zero or more of the previous character/group.

**Q4.** What does `+` mean?
**A:** One or more of the previous.

**Q5.** What does `?` mean?
**A:** Zero or one (makes the previous optional).

**Q6.** What does `^` match?
**A:** Start of the line/string.

**Q7.** What does `$` match?
**A:** End of the line/string.

**Q8.** What does `\d` match?
**A:** Any digit `[0-9]`.

**Q9.** What does `\w` match?
**A:** Any word character `[a-zA-Z0-9_]`.

**Q10.** What does `\s` match?
**A:** Any whitespace character.

### Section B: Character Classes

**Q11.** What does `[abc]` match?
**A:** Any one of a, b, or c.

**Q12.** What does `[^abc]` match?
**A:** Any character EXCEPT a, b, c.

**Q13.** What does `[a-z]` match?
**A:** Any lowercase letter.

**Q14.** What does `[0-9]{3}` match?
**A:** Exactly three digits.

### Section C: Quantifiers

**Q15.** Difference between `*` and `+`?
**A:** `*` = 0 or more; `+` = 1 or more.

**Q16.** What does `a{2,4}` match?
**A:** Between 2 and 4 "a"s.

**Q17.** What does `a?` match?
**A:** Zero or one "a".

### Section D: Groups & Alternation

**Q18.** What does `(cat|dog)` match?
**A:** Either "cat" or "dog".

**Q19.** What's the difference between `()` and `(?:...)`?
**A:** `()` captures the match; `(?:...)` doesn't.

**Q20.** Why do you need parentheses around `|`?
**A:** Because `|` has the lowest precedence; parentheses limit its scope.

### Section E: Lookarounds & Backreferences

**Q21.** What is a lookahead?
**A:** A zero-width assertion that checks if a pattern appears ahead.

**Q22.** What does `(?=...)` do?
**A:** Positive lookahead — requires `...` to be present.

**Q23.** What does `(\w+)\s+\1` match?
**A:** A repeated word (e.g., "hello hello").

### Section F: Real Patterns

**Q24.** Write a regex to match an IPv4 address.
**A:** `\b(?:\d{1,3}\.){3}\d{1,3}\b`

**Q25.** Write a regex to match a US ZIP code.
**A:** `\d{5}(-\d{4})?`

**Q26.** Write a regex to match a hex color.
**A:** `#(?:[0-9a-fA-F]{3}){1,2}`

---

## 21. Exam-Style Questions

**Q1.** What does the regex `^\d{3}-\d{4}$` match?
a) Any string
b) A phone number in XXX-XXXX format
c) A date
d) An email

**Answer: b**

---

**Q2.** What does `a*` match in the string "aaa"?
a) Only "a"
b) "", "a", "aa", "aaa"
c) Only "aaa"
d) Nothing

**Answer: b** (zero or more)

---

**Q3.** What does the regex `[^0-9]+` match?
a) Only digits
b) One or more non-digits
c) Zero or more digits
d) One or more digits

**Answer: b**

---

**Q4.** Difference between greedy and lazy matching?
a) There is no difference
b) Greedy matches as little as possible; lazy matches as much as possible
c) Greedy matches as much as possible; lazy matches as little as possible
d) Only greedy exists

**Answer: c**

---

**Q5.** Which flag makes `^` and `$` match at every line?
a) `i`
b) `g`
c) `m`
d) `s`

**Answer: c** (multiline)

---

**Q6.** What does `(?<=USD)\d+` match?
a) Digits followed by USD
b) Digits preceded by USD
c) Digits equal to USD
d) Nothing

**Answer: b**

---

**Q7.** Which is NOT supported in RE2 (Go)?
a) Character classes
b) Quantifiers
c) Backreferences
d) Anchors

**Answer: c**

---

**Q8.** What's the correct way to match a literal dot?
a) `.`
b) `\.`
c) `..`
d) `[.]` only

**Answer: b** (also `[.]` works)

---

**Q9.** What does `(?:abc)+` do?
a) Captures "abc"
b) Groups "abc" as non-capturing and matches one or more repetitions
c) Matches only "abc"
d) Throws an error

**Answer: b**

---

**Q10.** What is the difference between `\d` and `[0-9]`?
a) No difference
b) `\d` is faster
c) `\d` may match non-ASCII digits in Unicode mode
d) `[0-9]` matches letters

**Answer: c** (In Unicode-aware engines, `\d` can match digits from other scripts.)

---

## 22. Quick Reference Cheat Sheet

| Pattern | Meaning |
|---------|---------|
| `.` | Any character (except newline) |
| `\d` | Any digit `[0-9]` |
| `\D` | Any non-digit |
| `\w` | Word character `[a-zA-Z0-9_]` |
| `\W` | Non-word character |
| `\s` | Whitespace |
| `\S` | Non-whitespace |
| `^` | Start of line |
| `$` | End of line |
| `\b` | Word boundary |
| `\B` | Non-word boundary |
| `*` | 0 or more |
| `+` | 1 or more |
| `?` | 0 or 1 |
| `{n}` | Exactly n |
| `{n,}` | n or more |
| `{n,m}` | n to m |
| `*?`, `+?`, `??` | Lazy versions |
| `[...]` | Character class |
| `[^...]` | Negated class |
| `( )` | Capturing group |
| `(?: )` | Non-capturing group |
| `(?P<name>...)` | Named group |
| `\|` | Alternation (OR) |
| `\` | Escape |
| `(?=...)` | Positive lookahead |
| `(?!...)` | Negative lookahead |
| `(?<=...)` | Positive lookbehind |
| `(?<!...)` | Negative lookbehind |
| `\1`, `\2` | Backreference |
| `\A` | Start of string |
| `\z` | End of string |

### Common Flags

| Flag | Meaning |
|------|---------|
| `i` | Case-insensitive |
| `g` | Global |
| `m` | Multiline |
| `s` | Dotall |
| `x` | Extended (whitespace ignored) |

### Common Patterns

| Purpose | Pattern |
|---------|---------|
| Email | `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}` |
| IPv4 | `\b(?:\d{1,3}\.){3}\d{1,3}\b` |
| Date YYYY-MM-DD | `\d{4}-\d{2}-\d{2}` |
| URL | `https?://[^\s]+` |
| Hex color | `#(?:[0-9a-fA-F]{3}){1,2}` |
| Digits only | `^\d+$` |
| Letters only | `^[A-Za-z]+$` |
| Strong password | `^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$` |

### Command-Line Regex

| Tool | Regex Type | Notes |
|------|-----------|-------|
| `grep` | BRE | Escape `+`, `?`, `{}` |
| `grep -E` | ERE | Direct metacharacters |
| `grep -P` | PCRE | Full-featured |
| `sed` | BRE | Use `-E` for ERE |
| `awk` | ERE | Direct metacharacters |
| `ripgrep` | PCRE-ish | Fast, modern |
