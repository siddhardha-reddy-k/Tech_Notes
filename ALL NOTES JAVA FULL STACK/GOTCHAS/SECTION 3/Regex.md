# Step 1: The 4 String Methods (just the shape, no regex yet)

```java
str.matches(pattern)              // true/false — does WHOLE string fit the pattern?  
str.replaceAll(pattern, newText)  // replace ALL matches  
str.replaceFirst(pattern, newText)// replace only FIRST match  
str.split(pattern)                // break string into array  
```

### Step 2: Literal characters (simplest possible regex)

A regex with just plain letters matches those exact letters. No symbols yet.

```java
"cat".matches("cat");     // true  -> exact match  
"cat".matches("dog");     // false  
"cat".matches("ca");      // false -> matches() needs the WHOLE string, not part
```

Nothing fancy here. Understood? Now we add power one symbol at a time.

### Step 3: . — matches ANY one character

```java
"cat".matches("c.t");   // true  -> . matched 'a'  
"cot".matches("c.t");   // true  -> . matched 'o'  
"cbt".matches("c.t");   // true  -> . matched 'b'  
"ct".matches("c.t");    // false -> . must match exactly ONE character, but none exists here  
"caat".matches("c.t");  // false -> too many characters, . only covers ONE spot
```

So . = "any single character, exactly one slot." Nothing about "many" yet — that's next.

### Step 4: Quantifiers — HOW MANY times does the previous thing repeat?

This is the part you got confused on. A quantifier always applies to the single character/group right before it. Let's build it up one symbol at a time.

## ? — the thing before it appears 0 or 1 times (optional)

```java
"color".matches("colou?r");   // true  -> u appeared 0 times... wait let's check  
"colour".matches("colou?r");  // true  -> u appeared 1 time
```

Here u? means "u is optional." Both color and colour match.

* — the thing before it appears 0 or MORE times

```java
"ct".matches("ca*t");     // true  -> 'a' appeared 0 times  
"cat".matches("ca*t");    // true  -> 'a' appeared 1 time  
"caaat".matches("ca*t");  // true  -> 'a' appeared 3 times  
"cbt".matches("ca*t");    // false -> 'b' is not 'a', doesn't matter how many
```

a* means "zero or more a's." It does NOT mean "any character repeated" — only the specific thing right before the * repeats.

+ — the thing before it appears 1 or MORE times (this is the one I used too early last time)

```java
"ct".matches("ca+t");     // false -> need AT LEAST 1 'a', got 0  
"cat".matches("ca+t");    // true  -> 1 'a'  
"caaat".matches("ca+t");  // true  -> 3 a's, still fine
```

So a+ = "one or more a's." Difference from *: + requires at least 1, * allows 0.

## {n}, {n,}, {n,m} — exact/range counts

```java
"caat".matches("ca{2}t");     // true  -> exactly 2 a's  
"cat".matches("ca{2}t");      // false -> only 1 a, needed exactly 2  
"caaaat".matches("ca{2,4}t"); // true  -> 4 a's, within range 2 to 4  
"caaaaat".matches("ca{2,4}t");// false -> 5 a's, too many
```

Now going back to my earlier example: "[a-z]+" meant "one or more of anything in a-z." That + is exactly what you just learned — apply it to a character class, which is next.

### Step 5: Character classes [...] — pick from a set, still just ONE slot

```java
"c".matches("[abc]");     // true  -> c is in the set {a,b,c}  
"d".matches("[abc]");     // false -> d is not in the set  
"5".matches("[0-9]");     // true  -> range shorthand, 0 through 9  
"g".matches("[a-z]");     // true  -> range a through z
```

[...] by itself is still ONE character slot — same rule as ., just restricted to a set instead of "anything."

Now combine with quantifier, same rule as before — quantifier applies to whatever is immediately to its left:

```java
"hello".matches("[a-z]+");   // true -> "one or more chars from a-z" — NOW this makes sense  
"Hello".matches("[a-z]+");   // false -> H is uppercase, not in [a-z]  
"12345".matches("[0-9]+");   // true  
```

### Step 6: Predefined Character Classes — just shortcuts for common [...]

These save you from typing [0-9], [a-zA-Z0-9_] etc. every time. Still ONE slot, same quantifier rules apply.

\d   ==  [0-9]              // digit  
\D   ==  [^0-9]              // NOT a digit (^ inside [] means "opposite")  
\w   ==  [a-zA-Z0-9_]        // word char (letters, digits, underscore)  
\W   ==  [^a-zA-Z0-9_]        // NOT a word char  
\s   ==  [ \t\n\r]            // whitespace (space, tab, newline...)  
\S   ==  [^ \t\n\r]            // NOT whitespace

⚠️ In Java code you must double the backslash: "[\\d](file://d)" not "\d" (single \ in a Java string is an escape character for the string itself, so Java needs \\ to actually produce one \ for the regex engine).

## Examples — same drill as before:

```java
"5".matches("\\d");        // true  
"a".matches("\\d");        // false  
"12345".matches("\\d+");   // true -> one or more digits  
"12a45".matches("\\d+");   // false -> 'a' breaks it, whole string must match

"hello_123".matches("\\w+"); // true -> letters+digits+underscore all allowed  
"hello 123".matches("\\w+"); // false -> space is NOT a word char

"   ".matches("\\s+");     // true -> one or more whitespace  
"a b".matches("\\s+");     // false -> 'a' and 'b' aren't whitespace, whole string fails
```

That's really it — \d, \w, \s are just named shortcuts for [...] sets you already understand.

### Step 7: Anchors — ^ and $ (position, not a character)

Big mental shift: anchors don't match a character. They match a position in the string.

^   // means "start of string"  
$   // means "end of string"

Since matches() already forces whole-string matching, ^/$ don't add much with matches(). They matter a LOT with replaceAll() / split() where you're searching inside a bigger string, not matching the whole thing.

```java
"hello world".replaceAll("^h", "H");    
// "Hello world" -> only replaces h if it's at the START

"cat cat cat".replaceAll("cat$", "DOG");  
// "cat cat DOG" -> only replaces cat if it's at the END
```

## \b — word boundary (edge between word-char and non-word-char)

```java
"cat category".replaceAll("\\bcat\\b", "DOG");  
// "DOG category" -> only the standalone word "cat" replaced,  
// NOT the "cat" inside "category" because there's no boundary there
```

## Without \b:

```java
"cat category".replaceAll("cat", "DOG");  
// "DOG DOGegory" -> oops, matched inside "category" too
```

This \b example is a genuinely common interview/practical gotcha — "replace whole word only" always needs \b.

### Step 8: Groups ()

A group lets you treat multiple characters as ONE unit — so you can apply a quantifier to a whole chunk, not just one character.

```java
"hahaha".matches("(ha)+");   // true -> (ha) is one unit, repeated 3 times  
"haha".matches("ha+");        // false -> WITHOUT parens, + only applies to 'a', so this means h + (1 or more a's) -> doesn't match "haha"
```

This is the difference: ha+ vs (ha)+ — same rule as always, quantifier binds to whatever is immediately before it. Without (), that's just the last single character. With (), it's the whole group.

## Groups also let you capture and reuse a piece of the match:

```java
"aabb".replaceAll("(a)", "[$1]");  
// "[a][a]bb" -> $1 refers back to whatever group 1 captured
```

## Remember this one from earlier? Now it should make sense:

```java
"aaabbbccc".replaceAll("(.)\\1+", "$1");  
// (.)   -> capture any ONE character into group 1  
// [\\1+](file://1+)  -> one or more repeats of whatever group 1 captured  
// $1    -> in the replacement, put back just that one character  
// result: "abc"
```

### Step 9: Greedy vs Lazy

By default *, +, {n,m} are greedy — they grab as much as possible.

```java
"<a><b>".replaceAll("<.+>", "X");  
// "X" -> .+ greedily grabbed EVERYTHING from first < to the LAST >
```

Add a ? after the quantifier to make it lazy — grab as little as possible:

```java
"<a><b>".replaceAll("<.+?>", "X");  
// "XX" -> now it stops at the FIRST >, matches <a> and <b> separately
```

⚠️ Note: this ? is different from the earlier "0 or 1" ?. Here, ? right after another quantifier (+?, *?) means "be lazy instead of greedy." Context tells you which meaning applies.
