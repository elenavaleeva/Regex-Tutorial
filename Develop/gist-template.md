# Regex Tutorial

This tutorial is meant to be a foundational reference guide for anyone learning
regular expressions.
To write code, but also write about code, also searching the
web for tutorials about any of the subjects I've
learned so far in this course. Its likely to find thousands of tutorials written
by developers of all skill levels, including junior developers—like myself!

This assignment this week is to create a tutorial that explains how a specific
regular expression, or regex, functions by breaking
down each part of the expression and describing what it does. I'll use the
template provided in the starter code to create my walkthrough.

## Summary

A regular expression or "regex" is a statement that describes a specific pattern
of characters that can be searched
for in a file or directory, matched and returned to be utilized by a user or program
to serve various use cases.
The goal of each regex is to return a match for continuous characters. The type of
characters, number characters and order
of characters can all be specified and modified in the regex statement.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex for an email address

To get a valid email id use a regular expression

/^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)\*\$/.

Every email address consists of 3 elements: local-part, @ symbol (pronounced as “at”),
and domain name. The local-part is placed
before the @ symbol, and the domain name is placed after the @ symbol. For example,
in the email johndoe@company.com, “johndoe” is
the local-part, and “company.com” is the domain.

## Regex Components

### Anchors

Anchors. These are special sequences which match an empty substring:
.^ matches at the beginning of the target string
.\$ matches at the end of the target string
.\b matches on a word boundary, i.e., the previous or subsequent character is not a word character

### Quantifiers

Regular expressions use quantifiers to generate unbounded matching possibilities and other
matching amount specifications. An atom can optionally be followed by one of these quantifiers:

- representing 0 or more occurrences of the atom,

* representing 1 or more occurrence of the atom,
  ? representing 0 or 1 occurrences of the atom,
  the bound {n} representing exactly n occurrences of the atom,
  the bound {m,n} representing between m and n occurrences of the atom.
  The quantifier can optionally be followed by "?" indicating that the match be minimal
  (non-greedy, reluctant) as opposed to the default maximal (greedy) match.

  ## Full regular expressions

  An atom optionally followed by a quantifier is called a piece.
  The juxtaposition (concatenation) of pieces is called a branch. A target string matches a
  branch if some substring combination matches each corresponding piece.
  A regular expression is a choice of branches represented by a string where the branches are
  separated by the | character. A choice is matched if one or more of the branches match.
  For example, these are atoms:

a b [abc](a|b+c) [^bc]
these, in addition to all above, are pieces:
a* c+ (ca*b)* (a|b+c){3}
these, in addition to all above, are branches:
aba a*b* [ab]*c* (a|b+c){3,10}(b|a+c){4}
these, in addition to all above, are regular expressions:
a*b|ab* a|b+|c* ((ab|ba){3,10}[cd]|aa\*bc)+
Regular Expression usage
Regular expressions are used commonly in programming contexts for these four types of operations:
validate: determine if a string matches a pattern, giving a boolean (yes/no) result
extract: extract portion(s) of a string which match a pattern
substitute: substitute portion(s) of a string which match a pattern by a replacement string
split: remove portions which match a pattern, thereby obtaining a list of strings

### Grouping Constructs

Grouping constructs delineate the subexpressions of a regular expression and capture the
substrings of an input string. You can use grouping constructs to do the following:
Match a subexpression that is repeated in the input string.

Apply a quantifier to a subexpression that has multiple regular expression language elements.
For more information about quantifiers, see Quantifiers.

Include a subexpression in the string that is returned by the Regex.Replace and Match.Result
methods.

Retrieve individual subexpressions from the Match.Groups property and process them separately
from the matched text as a whole.

The following table lists the grouping constructs supported by the .NET regular expression
engine and indicates whether they are capturing or non-capturing.

### Bracket Expressions

A bracket expression (an expression enclosed in square brackets, "[]" ) is an RE that shall match a specific
set of single characters, and may match a specific set of multi-character collating elements, based on the
non-empty set of list expressions contained in the bracket expression.

### Character Classes

Character classes distinguish kinds of characters such as, for example, distinguishing between letters
and digits.

# JavaScript Demo: RegExp Character Classes

const chessStory = 'He played the King in a8 and she moved her Queen in c2.';
const regexpCoordinates = /\w\d/g;
console.log(chessStory.match(regexpCoordinates));
// Expected output: Array [ 'a8', 'c2']

const moods = 'happy 🙂, confused 😕, sad 😢';
const regexpEmoticons = /[\u{1F600}-\u{1F64F}]/gu;
console.log(moods.match(regexpEmoticons));
// Expected output: Array ['🙂', '😕', '😢']

### The OR Operator

Regex recognizes range expressions inside a list. They represent those characters that fall between
two elements in the current collating sequence. You form a range expression by putting a range operator
between two characters.
When attempting to build a logical “or” operation using regular expressions, we have a few approaches to follow.
Fortunately the grouping and alternation facilities provided by the regex engine are very capable, but when all
else fails we can just perform a second match using a separate regular expression – supported by the tool or
native language of your choice.

This functionality is simple enough, however, that it is not usually necessary to use higher programming
features to achieve logical “or.”

Logical “or” is more difficult to achieve using tools external to the regular expression engine itself, but
it is achievable by combining results of multiple regular expressions using the native “or” logical feature of
your programming language of choice. This can sometimes be simpler and easier for others to maintain in the future,
with only minimal performance impacts over moderate data-sets. In Java, for example:
Using Java conditionals to test string matches
import static org.junit.Assert.assertFalse;
import static org.junit.Assert.assertTrue;

import org.junit.Test;

public class RegexTest
{
@Test
public void testRegex()
{
assertTrue(stringMatches("I like dogs, but not lions."));
assertTrue(stringMatches("I like penguins, but not lions."));
assertFalse(stringMatches("I like lions, but not penguins."));
}

private boolean stringMatches(String string)
{
return (string.matches("like dogs") || string.matches("like penguins"))
&& (string.matches("not lions") || string.matches("not tigers"));
}

}

### Flags

A flag is an optional parameter to a regex that modifies its behavior of searching.

A flag is denoted using a single lowercase alphabetic character.

In JavaScript regex, we have a total of 6 flags, each serving a different purpose.

Flag Name Modification
i Ignore Casing Makes the expression search case-insensitively.
g Global Makes the expression search for all occurrences.
s Dot All Makes the wild character . match newlines as well.
m Multiline Makes the boundary characters ^ and \$ match the beginning and ending of every single line instead of the beginning and ending of the whole string.
y Sticky Makes the expression start its searching from the index indicated in its lastIndex property.
u Unicode Makes the expression assume individual characters as code points, not code units, and thus match 32-bit characters as well.

But how to add these flags to a regex?

Very simple...

For an expression created literally, i.e. using the forward slashes //, flags comes after the second slash. In general notation we can expression this as follows:

/pattern/flags
Similarly, for an expression created using RegExp(), flags go as a string in the second argument, as shown below:

new RegExp('pattern', 'flags')
For example, if we were to give the flag i to the regex /a/, we'd write /a/i. And similarly in the case of new RegExp('a'), we'd write new RegExp('a', 'i')

To give multiple flags to a regex, we write them one after another (without any spaces or other delimiters).

For example, if we were to give both the flags i and g to the regex /a/, we'd write /a/ig (or equivalently /a/gi, since the order doesn't matter).

### Character Escapes

The \ is known as the escape code, which restore the original literal meaning of the following character.
Similarly, \* , + , ? (occurrence indicators), ^ , \$ (position anchors) have special meaning in regex.
You need to use an escape code to match with these characters.

## Author

Author Elena Valeeva.

https://elenavaleeva.github.io/Regex-Tutorial/

https://github.com/elenavaleeva/Regex-Tutorial
