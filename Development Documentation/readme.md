
## Development basics for dictionary files
Firefox dictionary add-ons use the [GNU Aspell system](http://aspell.net/man-html/)
There are two files that make up the important function of the add-on. These are the `.dic` file and the `.aff` file 
The `.dic` file is the list of words contained in the spellchecking dictionary. The `.aff` file is a list of rules and additional options.


### Rules, Prefixes and Suffixes
Each rule is in the `.aff` file for that language. The rules come in two flavors: ***SFX*** for suffixes, and ***PFX*** for prefixes. Each line begins with PFX/SFX and then the rule letter identifier (the ones that follow the word in the dictionary file:

 - PFX *<rule_letter_identifier> <combinable_flag><number_of_rule_lines_that_follow>*

You can normally ignore the combinable flag, it is Y or N depending on whether it can be combined with other rules. Then there are some number of lines (indicated by the ) that list different possibilities for how this rule applies in different situations. It looks like this:

 - PFX *<rule_letter_identifier> <number_of_letters_to_delete><what_to_add> <when_to_add_it>*

**For example:**

    SFX B Y 3
    SFX B 0 able <^aeiou>
    SFX B 0 able ee
    SFX B e able <^aeiou>e

If B is one of the letters following a word, i.e. word/B, then this is one of the rules that can apply. There are three possibilities that can happen (because there are three lines). Only one will apply:

    able is added to the end when the end of the word is not (indicated by ^) one of the letters in the set (indicated by < >) of letters a, e, i, o, and u. For example, question → questionable
    able is added to the end when the end of the word is ee. For example, agree → agreeable.
    able is added to the end when the end of the word is not a vowel (<^aeiou>) followed by an e. The letter e is stripped (the column before able). For example, excite → excitable.

PFX rules are the same, but apply at the **beginning** of the word.



This information has been adapted from the following sources:
- [Chromium developers - Editing the spell checking dictionaries](https://sites.google.com/a/chromium.org/dev/developers/how-tos/editing-the-spell-checking-dictionaries)
- [Fun with Aspell lists](http://typethinker.blogspot.com/2008/02/fun-with-aspell-word-lists.html)
- [GNU Aspell 0.60.9-git](http://aspell.net/man-html/)
