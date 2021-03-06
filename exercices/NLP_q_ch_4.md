1. ☼ Find out more about sequence objects using Python's help facility. In the interpreter, type help(str), help(list), and help(tuple). This will give you a full list of the functions supported by each type. Some functions have special names flanked with underscore; as the help documentation shows, each such function corresponds to something more familiar. For example  x.__getitem__(y) is just a long-winded way of saying x[y].

```

help(str)
Help on class str in module builtins:

class str(object)
 |  str(object='') -> str
 |  str(bytes_or_buffer[, encoding[, errors]]) -> str
 |  
 |  Create a new string object from the given object. If encoding or
 |  errors is specified, then the object must expose a data buffer
 |  that will be decoded using the given encoding and error handler.
 |  Otherwise, returns the result of object.__str__() (if defined)
 |  or repr(object).
 |  encoding defaults to sys.getdefaultencoding().
 |  errors defaults to 'strict'.
 |  
 |  Methods defined here:
 |  
 |  __add__(self, value, /)
 |      Return self+value.
 |  
 |  __contains__(self, key, /)
 |      Return key in self.
 |  [...]


help(list)
Help on class list in module builtins:

class list(object)
 |  list() -> new empty list
 |  list(iterable) -> new list initialized from iterable's items
 |  
 |  Methods defined here:
 |  
 |  __add__(self, value, /)
 |      Return self+value.
 |  
 |  __contains__(self, key, /)
 |      Return key in self.
[...]

help(tuple)
Help on class tuple in module builtins:

class tuple(object)
 |  tuple() -> empty tuple
 |  tuple(iterable) -> tuple initialized from iterable's items
 |  
 |  If the argument is a tuple, the return value is the same object.
 |  
 |  Methods defined here:
 |  
 |  __add__(self, value, /)
 |      Return self+value.
 |  
 |  __contains__(self, key, /)
 |      Return key in self.
 [...]
 
```

2. ☼ Identify three operations that can be performed on both tuples and lists. Identify three list operations that cannot be performed on tuples. Name a context where using a list instead of a tuple generates a Python error.

This functions works on both lists and tuples (and strings, eksept then it will return tokens not words)

```
list = ['I', 'turned', 'off', 'the', 'spectroroute']
tuple = (6, 'turned')
list[3], tuple[1]
Out[225]: ('the', 'turned')

list[-3:], tuple[-3:]
Out[226]: (['off', 'the', 'spectroroute'], (6, 'turned'))

len(list), len(tuple)
Out[227]: (5, 2)

```

 This works on list, but not on tuples:
 
```
tuples.sort()
tuples[1] = ('turned', 'VBD', ['t3:nd', 't3`nd'])
del tuples[0]

```

This is because tuples are immutable, lists are not.


3. ☼ Find out how to create a tuple consisting of a single item. There are at least two ways to do this.

I only found one way to do this..

```
text= ('snark',)

type(text)
Out[244]: tuple

```
I tried 

```
text2 = ['handle', ' ']
type(text2)
Out[254]: list

text2 = tuple(text2)
Traceback (most recent call last):

  File "<ipython-input-255-c3cbc0cc30b6>", line 1, in <module>
    text2 = tuple(text2)

TypeError: 'tuple' object is not callable

```

4. ☼ Create a list words = ['is', 'NLP', 'fun', '?']. Use a series of assignment statements (e.g. words[1] = words[2]) and a temporary variable tmp to transform this list into the list  ['NLP', 'is', 'fun', '!']. Now do the same transformation using tuple assignment.

With list:

```
words = ['is', 'NLP', 'fun', '?']

words[0], words[1] = words[1], words[0]

words[3] = '!'

print (words)
['NLP', 'is', 'fun', '!']

words = ['is', 'NLP', 'fun', '?']
tmp = words[0]
words[0] = words[1]
words[1] = tmp
words[3] = '!'
print (words)
['NLP', 'is', 'fun', '!']

```
As expected since tuples are immutable this did not work:

```
words = ('is', 'NLP', 'fun', '?')

type(words)
Out[279]: tuple

words[0], words[1] = words[1], words[0]

words[3] = '!'

print (words)

Traceback (most recent call last):

  File "<ipython-input-280-d485795ae33a>", line 1, in <module>
    words[0], words[1] = words[1], words[0]

TypeError: 'tuple' object does not support item assignment


```


5. ☼ Read about the built-in comparison function cmp, by typing help(cmp). How does it differ in behavior from the comparison operators?

```

help(cmp)
Traceback (most recent call last):

  File "<ipython-input-9-a687b1e1e9d3>", line 1, in <module>
    help(cmp)

NameError: name 'cmp' is not defined

```

found this: "As mentioned in the comments, cmp doesn't exist in Python 3" (https://stackoverflow.com/questions/22490366/cmp-isnt-woking-for-me-python?answertab=active#tab-top)

6. ☼ Does the method for creating a sliding window of n-grams behave correctly for the two limiting cases: n = 1, and n = len(sent)?

Sorry, don't understand the question..

```
sent = ['The', 'dog', 'gave', 'John', 'the', 'newspaper']

n = 3

[sent[i:i+n] for i in range(len(sent)-n+1)]
Out[23]: 
[['The', 'dog', 'gave'],
 ['dog', 'gave', 'John'],
 ['gave', 'John', 'the'],
 ['John', 'the', 'newspaper']]

n = 1

[sent[i:i+n] for i in range(len(sent)-n+1)]
Out[25]: [['The'], ['dog'], ['gave'], ['John'], ['the'], ['newspaper']]

n = len(sent)

[sent[i:i+n] for i in range(len(sent)-n+1)]
Out[27]: [['The', 'dog', 'gave', 'John', 'the', 'newspaper']]

``` 

7. ☼ We pointed out that when empty strings and empty lists occur in the condition part of an if clause, they evaluate to False. In this case, they are said to be occurring in a Boolean context. Experiment with different kind of non-Boolean expressions in Boolean contexts, and see whether they evaluate as True or False.

Don't know what i'm suppose to do here :P

```
sent = ['No', 'good', 'fish', 'goes', 'anywhere', 'without', 'a', 'porpoise', '.']

all(len(w) > 4 for w in sent)
Out[29]: False

any(len(w) > 4 for w in sent)
Out[30]: True

if 'Yes' in sent:
     print(1)
elif 'fish' in sent:
     print(2)
2

```

8. ☼ Use the inequality operators to compare strings, e.g. 'Monty' < 'Python'. What happens when you do 'Z' < 'a'? Try pairs of strings which have a common prefix, e.g.  'Monty' < 'Montague'. Read up on "lexicographical sort" in order to understand what is going on here. Try comparing structured objects, e.g. ('Monty', 1) < ('Monty', 2). Does this behave as expected?


It sort alphabeticaly, and don't care about capital letters

``` 
'Monty' < 'Python'
Out[35]: True

'Z' < 'a'
Out[36]: True

'z' < 'A'
Out[46]: False

'A' < 'z'
Out[47]: True

'Monty' < 'Montague'
Out[37]: False

('Monty', 1) < ('Monty', 2)
Out[38]: True 

('Monty', 2) < ('Monty', 1)
Out[45]: False

'abc' < 'ab'
Out[39]: False

'ab' < 'abc'
Out[40]: True

'dog' < 'underdog'
Out[41]: True

'dog' > 'underdog'
Out[42]: False

``` 

9. ☼ Write code that removes whitespace at the beginning and end of a string, and normalizes whitespace between words to be a single space character.

do this task using split() and join()
do this task using regular expression substitutions

10. ☼ Write a program to sort words by length. Define a helper function cmp_len which uses the cmp comparison function on word lengths.

11. ◑ Create a list of words and store it in a variable sent1. Now assign sent2 = sent1. Modify one of the items in sent1 and verify that sent2 has changed.

Now try the same exercise but instead assign sent2 = sent1[:]. Modify sent1 again and see what happens to sent2. Explain.
Now define text1 to be a list of lists of strings (e.g. to represent a text consisting of multiple sentences. Now assign text2 = text1[:], assign a new value to one of the words, e.g.  text1[1][1] = 'Monty'. Check what this did to text2. Explain.
Load Python's deepcopy() function (i.e. from copy import deepcopy), consult its documentation, and test that it makes a fresh copy of any object.

12. ◑ Initialize an n-by-m list of lists of empty strings using list multiplication, e.g. word_table = [[''] * n] * m. What happens when you set one of its values, e.g.  word_table[1][2] = "hello"? Explain why this happens. Now write an expression using range() to construct a list of lists, and show that it does not have this problem.

13. ◑ Write code to initialize a two-dimensional array of sets called word_vowels and process a list of words, adding each word to word_vowels[l][v] where l is the length of the word and v is the number of vowels it contains.

14. ◑ Write a function novel10(text) that prints any word that appeared in the last 10% of a text that had not been encountered earlier.

15. ◑ Write a program that takes a sentence expressed as a single string, splits it and counts up the words. Get it to print out each word and the word's frequency, one per line, in alphabetical order.

16. ◑ Read up on Gematria, a method for assigning numbers to words, and for mapping between words having the same number to discover the hidden meaning of texts (http://en.wikipedia.org/wiki/Gematria, http://essenes.net/gemcal.htm).

Write a function gematria() that sums the numerical values of the letters of a word, according to the letter values in letter_vals:

 	
>>> letter_vals = {'a':1, 'b':2, 'c':3, 'd':4, 'e':5, 'f':80, 'g':3, 'h':8,
... 'i':10, 'j':10, 'k':20, 'l':30, 'm':40, 'n':50, 'o':70, 'p':80, 'q':100,
... 'r':200, 's':300, 't':400, 'u':6, 'v':6, 'w':800, 'x':60, 'y':10, 'z':7}
Process a corpus (e.g. nltk.corpus.state_union) and for each document, count how many of its words have the number 666.

Write a function decode() to process a text, randomly replacing words with their Gematria equivalents, in order to discover the "hidden meaning" of the text.

17. ◑ Write a function shorten(text, n) to process a text, omitting the n most frequently occurring words of the text. How readable is it?

18. ◑ Write code to print out an index for a lexicon, allowing someone to look up words according to their meanings (or pronunciations; whatever properties are contained in lexical entries).

19. ◑ Write a list comprehension that sorts a list of WordNet synsets for proximity to a given synset. For example, given the synsets minke_whale.n.01, orca.n.01, novel.n.01, and  tortoise.n.01, sort them according to their shortest_path_distance() from right_whale.n.01.

20. ◑ Write a function that takes a list of words (containing duplicates) and returns a list of words (with no duplicates) sorted by decreasing frequency. E.g. if the input list contained 10 instances of the word table and 9 instances of the word chair, then table would appear before chair in the output list.

21. ◑ Write a function that takes a text and a vocabulary as its arguments and returns the set of words that appear in the text but not in the vocabulary. Both arguments can be represented as lists of strings. Can you do this in a single line, using set.difference()?

22. ◑ Import the itemgetter() function from the operator module in Python's standard library (i.e. from operator import itemgetter). Create a list words containing several words. Now try calling: sorted(words, key=itemgetter(1)), and sorted(words, key=itemgetter(-1)). Explain what itemgetter() is doing.

23. ◑ Write a recursive function lookup(trie, key) that looks up a key in a trie, and returns the value it finds. Extend the function to return a word when it is uniquely determined by its prefix (e.g. vanguard is the only word that starts with vang-, so lookup(trie, 'vang') should return the same thing as lookup(trie, 'vanguard')).

24. ◑ Read up on "keyword linkage" (chapter 5 of (Scott & Tribble, 2006)). Extract keywords from NLTK's Shakespeare Corpus and using the NetworkX package, plot keyword linkage networks.

25. ◑ Read about string edit distance and the Levenshtein Algorithm. Try the implementation provided in nltk.edit_distance(). In what way is this using dynamic programming? Does it use the bottom-up or top-down approach? [See also http://norvig.com/spell-correct.html]

26. ◑ The Catalan numbers arise in many applications of combinatorial mathematics, including the counting of parse trees (6). The series can be defined as follows: C0 = 1, and Cn+1 = Σ0..n (CiCn-i).

Write a recursive function to compute nth Catalan number Cn.
Now write another function that does this computation using dynamic programming.
Use the timeit module to compare the performance of these functions as n increases.
★ Reproduce some of the results of (Zhao & Zobel, 2007) concerning authorship identification.

★ Study gender-specific lexical choice, and see if you can reproduce some of the results of http://www.clintoneast.com/articles/words.php

★ Write a recursive function that pretty prints a trie in alphabetically sorted order, e.g.:

chair: 'flesh'
---t: 'cat'
--ic: 'stylish'
---en: 'dog'
