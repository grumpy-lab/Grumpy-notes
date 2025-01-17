#cheatsheets

#links are not working becuse im dumb 
✽ [Anchors](#anchors)  
✽ [Alternation and Grouping](#[alternation%20and%20grouping](https://github.com/grumpy-lab/Grumpy-notes/edit/main/cheatsheets/Regex.md#alternation-and-grouping)) 
✽ [Escaping meta characters](#Escaping%20meta%20characters)  
✽ [Dot meta character and Quantifiers](#dot%20meta%20character%20and%20quantifiers) 
✽ [Character class](#character%20class)  
✽ [Escape sequences](#escape-sequences)  
✽ [Named character sets](#named%20character%20sets)  
✽ [Backreferences](#backreferences)  
✽ [sed flags](#sed%20flags)  
✽ [sed case conversion](#sed%20case%20conversion)  
✽ [sed delimiters](#sed%20delimiters)  

  
  
## Anchors

|Pattern|Description|
|---|---|
|`^`|restricts the match to the start of the string|
|`$`|restricts the match to the end of the string|
|`\<`|restricts the match to the start of word|
|`\>`|restricts the match to the end of word|

The `-x` cli option in `grep` is equivalent to `^pattern$`.

Word characters include alphabets, digits and underscore. Here's some more alternate ways to specify word anchors:

|Pattern|Description|
|---|---|
|`\b`|restricts the match to the start/end of words, applicable for `grep` and `sed`|
|`\y`|restricts the match to the start/end of words, applicable for `awk` (`\b` means backspace)|
|`\B`|matches wherever `\b` (or `\y`) doesn't match|

`grep` also supports `-w` cli option. It is equivalent to `(?<!\w)pattern(?!\w)`. The three different ways to specify word anchors are not exactly equivalent though.

  

## Alternation and Grouping

|Pattern|Description|
|---|---|
|`pat1\|pat2\|pat3`|match `pat1` or `pat2` or `pat3`|
||use `\\|` in BRE mode|
|`()`|group pattern(s), `a(b\|c)d` is same as `abd\|acd`|
||use `\(\)` in BRE mode|

The alternative patterns can have their own independent anchors. Alternative which matches earliest in the input gets precedence. Longest matching portion wins if multiple alternatives start from the same location (irrespective of the order of alternatives). In case of a tie with same lengths, leftmost alternative wins

  

## Escaping meta characters 

|Pattern|Description|
|---|---|
|`\`|prefix metacharacters with `\` to match them literally|
|`\\`|to match `\` literally|

- With `grep` and `sed`, switching between ERE and BRE can reduce the number of escapes needed for some cases. For fixed string matching, `grep` has `-F` option and `awk` has string comparison operators (whole string) and the `index` function (partial string).
- `sed` requires both `(` and `)` characters to be escaped (in ERE mode), whereas `grep` and `awk` don't require `)` to be escaped.
- `sed` requires `{` to be escaped (in ERE mode) even if it isn't part of a valid quantifier syntax, whereas `grep` and `awk` don't require escaping. For example, you'd need `\{a}` in `sed` whereas `{a}` is enough for the other two.
- In BRE mode, `grep` and `sed` don't require `^` and `$` to be escaped if they are used away from their customary positions.

  

## Dot meta character and Quantifiers

|Pattern|Description|
|---|---|
|`.`|match any character, including the newline character|
|`?`|match `0` or `1` times|
||use `\?` in BRE mode|
|`*`|match `0` or more times|
|`+`|match `1` or more times|
||use `\+` in BRE mode|
|`{m,n}`|match `m` to `n` times|
|`{m,}`|match at least `m` times|
|`{,n}`|match up to `n` times (including `0` times)|
|`{n}`|match exactly `n` times|
||use `\{\}` in BRE mode|
|`pat1.*pat2`|any number of characters between `pat1` and `pat2`|
|`pat1.*pat2\|pat2.*pat1`|match both `pat1` and `pat2` in any order|

Precedence rule is _longest match wins_, which is mostly similar but not exactly same as greedy quantifiers. For example, with `foo123312baz` as input string, `o[123]+(12baz)?` will match `o123312baz` with these tools, whereas it will match `o123312` with greedy quantifiers.

  

## Character class

|Pattern|Description|
|---|---|
|`[set123]`|match any of these characters once|
|`[^set123]`|match except any of these characters once|
|`[3-7AM-X]`|range of characters from `3` to `7`, `A`, another range from `M` to `X`|
|`[.`|open collating symbol|
|`.]`|close collating symbol|
|`[=`|open equivalence class|
|`=]`|close equivalence class|

Specific placement will help to match character class metacharacters literally.

|Pattern|Description|
|---|---|
|`[a-z-]`|`-` should be first/last character to match literally|
|`[+^]`|`^` shouldn't be first character|
|`[]=]`|`]` should be first character (second if `^` is used to invert the set)|

- `\` isn't special within character class in `grep`.
- `\` can be used to escape character class metacharacters in `awk`.

Some commonly used character sets have predefined escape sequences:

|Pattern|Description|
|---|---|
|`\w`|similar to `[a-zA-Z0-9_]` for matching word characters|
|`\s`|similar to `[ \t\n\r\f\v]` for matching whitespace characters|
|`\W`|match non-word characters|
|`\S`|match non-whitespace characters|

- Undefined escape sequences will be treated as the character it escapes. For example, `\e` will match `e` (not `\` and `e`).
    - in addition, `awk` gives a "not a known regexp operator" warning.
- The above escape sequences _cannot_ be used inside character classes and behavior varies between the tools.
    - For example, using `[\w]` will match `\` or `w` characters in `grep` and `sed` whereas it will match only `w` in `awk`.
- These escape sequences are also locale aware, for example `αλεπού` and `\u2028` (line separator) will be considered as word and whitespace characters respectively in appropriate locales.
- These tools do _not_ support `\d` and `\D`, commonly featured in other regexp implementations for digits and non-digits.

  

## Escape sequences

This section is applicable only for `sed` and `awk` unless otherwise specified and can be used within character classes too. See also [ASCII Codes Table Standard characters](https://ascii.cl/).

|Escape sequence|Description|
|---|---|
|`\a`|alert|
|`\b`|backspace in `awk`, word boundary in `grep` and `sed`|
||`\b` inside a character class in `sed` will act as a backspace|
|`\f`|formfeed|
|`\n`|newline|
|`\r`|carriage return|
|`\t`|horizontal tab|
|`\v`|vertical tab|
|`\cx`|CONTROL-x in `sed`|

You can also represent ASCII characters using their codepoint values.

|Escape sequence|Description|
|---|---|
|`\xNN`|hexadecimal digits|
|`\NNN`|octal digits in `awk`|
|`\oNNN`|octal digits in `sed`|
|`\dNNN`|decimal digits in `sed`|

- In search section, a metacharacter specified by escape sequences will still act as the metacharacter. For example, `/\x5eco/` will match `co` only at the start of the string.
- In replacement section,
    - escape sequences in `sed` produces literal character. For example, `s/.*/"\x26"/` will have `"&"` as the replacement value.
    - escape sequences in `awk` is treated as metacharacter. For example, `sub(/.*/, "[&]")` and `sub(/.*/, "[\x26]")` are equivalent.


  

## Named character sets

The below table lists named sets and their equivalent character class in ASCII encoding. These can be used inside character classes only. For example, `[[:digit:]]` is same as `[0-9]` and `[[:alnum:]_]` is equivalent to `\w`.

|Named set|Description|
|---|---|
|`[:digit:]`|`[0-9]`|
|`[:lower:]`|`[a-z]`|
|`[:upper:]`|`[A-Z]`|
|`[:alpha:]`|`[a-zA-Z]`|
|`[:alnum:]`|`[0-9a-zA-Z]`|
|`[:xdigit:]`|`[0-9a-fA-F]`|
|`[:cntrl:]`|control characters — first 32 ASCII characters and 127th (DEL)|
|`[:punct:]`|all the punctuation characters|
|`[:graph:]`|`[:alnum:]` and `[:punct:]`|
|`[:print:]`|`[:alnum:]`, `[:punct:]` and space|
|`[:blank:]`|space and tab characters|
|`[:space:]`|whitespace characters, same as `\s`|

> Their interpretation depends on the `LC_CTYPE` locale; for example, `[[:alnum:]]` means the character class of numbers and letters in the current locale.

  

## Backreferences

|Pattern|Description|
|---|---|
|`\N`|backreference, gives matched portion of Nth capture group|
||possible values: `\1`, `\2` up to `\9`|
|`&`|represents entire matched string in the replacement section|
|`\0`|equivalent to `&` in `sed`|

Notes for `awk`:

- backreferences can be used only in replacement section, not allowed in search section.
- `sub` and `gsub` functions allow only the `&` backreference.
- `gensub` function allows `\N` form of backreference as well.
    - but need to use `\\0`, `\\1`, `\\2` etc since they are specified using string syntax.

  

## sed flags

This section discusses flags (also known as modifiers) that change the regexp behavior. When used with regexp addressing:

|Flag|Description|
|---|---|
|`I`|match case insensitively|

When used with substitution command:

|Flag|Description|
|---|---|
|`i` or `I`|match case insensitively|
|`g`|replace all occurrences instead of just the first match|
|`N`|a number will cause only the _N_th match to be replaced|
|`Ng`|replace from _N_th match to the end|
|`m` or `M`|multiline mode|
||`.` will not match the newline character|
||`^` and `$` will match every line's start and end locations (line separator is `\n` by default and NUL when `-z` option is used)|
|`` \` ``|always match the start of string irrespective of multiline mode|
|`\'`|always match the end of string irrespective of multiline mode|

Flags are not supported by `grep` or `awk`. But these equivalent/alternative options can be used:

- `-i` cli option in `grep` and setting `IGNORECASE` to non-zero value in `awk` will match case insensitively.
- `tolower` or `toupper` functions can be used in `awk` to convert input to single case.
- you can also use character classes for small strings, for example `[cC][aA][tT]` will match `cat` case insensitively.
- `sub` function in `awk` replaces only the first matching occurrence and `gsub` function is equivalent to using the `g` flag.
- third argument of `gensub` function in `awk` supports replacing only the _N_th match as well as the `g` flag.

The behavior of `sed` and `awk` differs for _N_th match if the pattern can match empty string:

```ruby
$ echo 'a,,c,d,,f' | sed 's/[^,]*/b/2'
a,b,c,d,,f
$ echo 'a,,c,d,,f' | sed 's/[^,]*/e/5'
a,,c,d,e,f

$ echo 'a,,c,d,,f' | awk '{print gensub(/[^,]*/, "b", 2)}'
ab,,c,d,,f
$ echo 'a,,c,d,,f' | awk '{print gensub(/[^,]*/, "e", 5)}'
a,,ce,d,,f
```

  

## sed case conversion

|Escape sequence|Description|
|---|---|
|`\E`|indicates end of case conversion in replacement section|
|`\l`|convert next character to lowercase|
|`\u`|convert next character to uppercase|
|`\L`|convert following characters to lowercase, stops if `\U` or `\E` is found|
|`\U`|convert following characters to uppercase, stops if `\L` or `\E` is found|

  

## sed delimiters

- `/` is idiomatically used as the delimiter.
- Any character except `\` and newline character can also be used. For example: `s#/home/learnbyexample/#~/#` is same as `s/\/home\/learnbyexample\//~\//`.
- For regexp addressing, the first delimiter has to be escaped. For example: `\;/foo/bar/;p` is same as `/foo\/bar\//p`.
