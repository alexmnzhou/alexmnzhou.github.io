---
id: 2064
title: Vocabulary Games
date: 2018-11-10T14:41:05+00:00
author: Alex Z.
layout: post
guid: https://www.physicstomato.com/?p=2064
permalink: /vocabulary-games/
views:
  - 136
image: /wp-content/uploads/2019/01/Similar-Words-Picture-1200x700.png
categories:
  - Executables
  - Idea Space
tags:
  - code
  - games
  - vocabulary
---
 

<hr class="wp-block-separator" />

Hi there! Long time no see.

Let’s play a game.&nbsp;

I’m going to give you all the vowels of a word, but none of the consonants. Instead of those, I&#8217;m putting empty spaces. The empty spaces are precise—if there&#8217;s only one space, there&#8217;s only one missing consonant. If two, then two. Then&nbsp;you’re going to guess which word I started with.

Here&#8217;s an example:

_ _ e _ e

There. What do you think it is?

Oops. I’ve already given it away. It&#8217;s the first word I used after showing you the puzzle. That’s the word I intended to be the solution, at least.

But you probably realized that a lot of other words could&#8217;ve worked too. You could’ve answered “where,” “scene,” “theme,” “these,” “crepe,” “abele,” or “prese.” All of those fit the vowel scheme I wrote down (some more possible answers [here](http://itools.subhashbose.com/wordfind/ending-with/e_e/no-of-letters_equal-to_5)).

As a side note, “niece” or “sieve” would not have worked, since I would’ve had to show you the “i.” The link I just gave you also includes some of these false positives.

Let’s try a more difficult and interesting vowel scheme, which only has one common solution (a few, technically, but they all share the same root).

  1. _ eio _ i _ e _  
    

Hope you like chemistry (all the answers are at the bottom, if you want to check).

There are some interesting properties to this game.

First, the amount of possible solutions to a given vowel scheme is pretty unpredictable. It follows the obvious pattern of more common vowels usually giving more possible combinations, but their placement matters too.

As a general rule, the simpler the scheme and the less specification, the more words can fit it, up to a point. Vowel schemes that include common combos like

o _ _ e (-orne, -ople, -ophe, -orse)

a _ e (-ane, -ace, -ale)

_ io _ (-tion, -cion, -sion)

also tend to have higher word counts.

In fact, one of the best vowel schemes I found for maximizing possible words is (note it includes a super common a _ e ):

_ a _ e _

Imagine capturing all the countless verbs that would fit the first four letters of that scheme and then effectively tripling that number (e.g. baked, bakes, baker). Then add all the other possibilities.

In cryptographic terms, every empty space adds about 20 more degrees of entropy (since y is usually used as a vowel). This isn&#8217;t quite a code, though, so the comparison isn&#8217;t great. Vowel scheme solutions always have to be actual words.

Increasing empty space is a good idea to increase the amount of combinations, but again, only up to a point. Few words have three consonants in a row unless the structure is designed to allow for them (coincidentally, the word “three” is part of one such structure) and even fewer have four in a row. Also, multi-letter combos generally have to follow a set of structures which, depending on the word, might end up giving less possibilities than just a single letter (e.g. “tr”, “ch”, “qu”, etc. for two letters).

So changing word length in general is unpredictable, unless you’re at an extreme low or high. Take, for example:

_ o

which can clearly only ever have up to 20 or 21 solutions for all the consonants and possibly ‘y’.

On the other extreme end, you have:

<ol start="2">
  <li>
    _ e _ i _ e _ i _ e _ i _ ua _ e _
  </li>
</ol>

or

<ol start="3">
  <li>
    _ _ o _ _ i _ a u _ i _ i _ i _ i _ i _ i _ i _ a _ i o _
  </li>
</ol>

Which are so long and convoluted that even without having any idea of the actual word, you can see they should clearly define only one solution (this time I’m sure of it).

But (and you guessed it) there are still exceptions. Some oddly long and specific designations can actually allow for way more words than you might expect. Take, for example:

<ol start="4">
  <li>
    _ u _ _ i _ a _ io _
  </li>
</ol>

How many solutions can you find? Once you get one, the others follow a similar sort of pattern, and you&#8217;ll start to see why it supports so many words relative to other vowel schemes of its length.

I&#8217;m thinking that even a machine learning/natural language processing solution would have trouble predicting the amount of combinations a given vowel scheme will have. The structure of words feels too unpredictable and organic. I could totally be wrong and I still want to try, but that’s for another day.

### Similar Words

<hr class="wp-block-separator" />

The title of this post is vocabulary games. That&#8217;s plural. I&#8217;ve only got two, but I saved the best for last:

Try to find a word where simply switching one letter drastically changes the meaning. Bonus points for using longer words.

This doesn&#8217;t have that many interesting properties (granted, it’s not even really a game), but it can be pretty funny.

Attaching and attacking.

Altercation and alternation.

Clinginess and cringiness.

Heroes and herpes.

Morphine and morphing.

Artistic and autistic.

Revenge and revenue.

There&#8217;s a lot of these in English. Find your own.

OR you can write a program to find every pair of English words that are just a single letter apart. I did this, actually.

About a year ago, a friend of mine came up with this &#8220;game&#8221; and I wanted to take it to its logical end. It took a lot of lines of Python code and a long time to run. Recently, I revisited the project and tried to improve on it with all the programming knowledge I&#8217;ve gained over that year:

First, just for bragging rights, I can now do this in&nbsp;_one_ line.

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">match_dict = {'length_%s_matches'%str(length):[comb for comb in itertools.combinations([w for w in [line.rstrip('\n') for line in open("words.txt", encoding="utf8")] if len(w) == length],2) if len(comb[0])-len([l1 for l1, l2 in zip(*comb) if l1==l2])==1] for length in [7,8,9,10,11,12,13,14,15,16,17,18,19,20]} </pre>

This is not a readable, editable, or in any sense advisable way to write code. But when I started shortening it, I immediately wanted know know if this was possible. There you go. All the words would be saved into &#8220;match\_dict&#8221; with the keys being &#8220;length\_[7,8,9,etc..]_matches&#8221;.

Here&#8217;s a better method that has readable code:

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">words = [line.rstrip('\n') for line in open("words.txt", encoding="utf8")] #Removes the line dilineator \n while formatting it into a list called 'lines'
accepted_lengths = [7,8,9,10,11,12,13,14,15,16,17,18,19,20]

def match_finder(array):
    return [comb for comb in itertools.combinations(array,2) if len(comb[0])-len([l1 for l1, l2 in zip(*comb) if l1==l2])==1]

length_dict = {"length_%s_list"%str(length):[w for w in words if len(w) == length] for length in accepted_lengths}
match_dict = {'length_%s_matches'%str(length):match_finder(length_dict['length_%s_list'%str(length)]) for length in accepted_lengths}</pre>

And here&#8217;s one way to format it into a single file:

<pre class="brush: python; collapse: false; title: ; wrap-lines: false; notranslate" title="">with open('Similar Words.txt','w') as similarwords:
    for length in accepted_lengths:
        similarwords.write('### Similar Words of Length %s ###\n\n'%length)
        for pair in match_dict['length_%s_matches'%length]:
            similarwords.write("%s and %s\n" %(pair[0].capitalize(),pair[1].capitalize()))
        similarwords.write('\n\n\n')</pre>

If you want to run it yourself, you&#8217;re also going to need a list complete with all 400000-odd English words. You can find one online pretty easily, but [I got you covered](https://www.physicstomato.com/wp-content/uploads/2019/01/words.txt).

Here are the [results](https://www.physicstomato.com/wp-content/uploads/2019/01/Similar-Words.txt) if you just want to look at those. There’s too much to sort through by myself, so have a look and let me know if you find anything good that I missed.

That’s all my games for now. Happy word-ing.

### Answers

<hr class="wp-block-separator" />

  1. Deionized, deionizes, deionizer (Bonus solution: [Meionites](https://en.wikipedia.org/wiki/Meionite)).
  2. Hemidemisemiquaver (Semidemisemiquaver is an alternate spelling, but I don&#8217;t count it as unique).
  3. Floccinaucinihilipilification (Fun fact: this has the most &#8220;consonant + i groups&#8221; in a row of any word).
  4. Duplication, culmination, publication, lubrication, sublimation, etc.