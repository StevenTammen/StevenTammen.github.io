---
permalink: /keyboard-layouts/
layout: layout
title: Keyboard Layouts
---

<div class="center">

   <h1>Keyboard Layouts</h1>
   
   <a href="https://github.com/StevenTammen/steventammen.github.io/edit/master/pages/keyboard-layouts.md" target="_blank">
     <img src="https://steventammen.github.io/assets/images/GitHub.png" height="30" width="30">
   </a> &nbsp; &nbsp;
   
   <a href="http://prose.io/#StevenTammen/steventammen.github.io/edit/master/pages/keyboard-layouts.md" target="_blank">
     <img src="https://steventammen.github.io/assets/images/Prose.png" height="30" width="30">
   </a>
   
</div>

<br/>

<div class="center">
   <img src="/assets/images/keyboard-layouts/base.png"><br/><br/>
   <img src="/assets/images/keyboard-layouts/shift.png"><br/><br/>
   <img src="/assets/images/keyboard-layouts/num.png"><br/><br/>
   <img src="/assets/images/keyboard-layouts/code.png"><br/><br/>
   <img src="/assets/images/keyboard-layouts/sym.png"><br/><br/>
   <img src="/assets/images/keyboard-layouts/func.png"><br/><br/>
   <img src="/assets/images/keyboard-layouts/media.png"><br/><br/>
</div>

## Prior Studies of Keyboard Layouts

I suggest you go through the following links (and any of the others from [this link](http://mdickens.me/typing/alternative_layouts.html) that catch your eye -- some of the links are dead) before you continue reading my approach, just so you can see what else is out there:

- [CarpalX](http://mkweb.bcgsc.ca/carpalx/)
- [MTGAP](https://mathematicalmulticore.wordpress.com/the-keyboard-layout-project/)
- [Aus der Neo Welt (AdNW)](http://adnw.de/) (and its [Google Group](https://groups.google.com/forum/#!forum/adnw))
- [The Optimal Keyboard Layout Project](http://web.archive.org/web/20041012232707/http://www.pvv.org/~hakonhal/main.cgi/keyboard/optimal/) (web archived)
- [Keyboard Evolve](http://www.michaelcapewell.com/programming/keyboardevolve.htm)
- [Norman](https://normanlayout.info/about.html)
- [Workman](http://workmanlayout.org/)
- [Maltron](http://www.adnw.de/uploads/Main/Malt-Artikel/Malt-Artikel.pdf)

There are no doubt other sites out there that discuss these things. I certainly do not pretend to be the first nor most intelligent person that has ever worked on this problem, and wouldn't want anyone to get that impression. Of the methodology of the sites above, I like AdNW and MTGAP best. I'm planning on writing about all the parameters and a logical weighting scheme at some point. (See the outline below).

## Base Layer

The first step to designing a base layer is getting a letter layout. There are many different options that have been created over the years, and several optimizers that have been designed to create them (CarpalX, AdNW, MTGAP). I will be using the statistics from the AdNW C++ optimizer to compare layouts since I believe it is the most thorough program available for comparison at the current time. I haven't tweaked any of the evaluation parameters (like positional penalties or adjacency penalties) but plan to eventually (since I type on a Kinesis Advantage and think that adjacency is OK as long as the motion in in-out and does not involve the pinky and ring finger together).

To be able to run the AdNW optimizer, you’ll need to compile the C++ source. I used [MinGW](http://mingw.org/), which is a Windows port of the GCC (GNU Compiler Collection, for C, C++, ADA, etc.). You’ll need to be a little bit familiar with the command line (e.g., changing directories), but it’s not too bad. I knew virtually nothing about compilers or running commands and figured out how to do it via Google and trial-and-error in like 20 minutes. I’ll try and get around posting a step-by-step guide at some point. (At least for Windows).

Once you have opt.cc compiled into opt.exe, it’s pretty easy to compare layouts according to AdNW’s digram and trigram statistics. However, I’d recommend you read through the English section of the instructions for the optimizer (Anleitung.pdf) anyway to get some of the theoretical background behind how optimization and comparison proceeds.

Before I compared the letter layouts, I changed the character set in standard.cfg to exclude punctuation entirely. I did this to compare letter layouts only. The optimizer needs "placeholder" characters, so I gave it characters that shouldn't appear in an English corpus (like 



You’ll also need to change the character set in standard.cfg (unless you type German and want the default characters). Here are the lines I changed:

```
Zeichen 'äÄ'
Zeichen 'öÖ'
Zeichen 'üÜ'
Zeichen '.'           # Nur ein Zeichen auf dieser Taste.
Zeichen ','           # Only one symbol on this key.
Zeichen 'ß'

```

And what I changed them into:

```

Zeichen !'!
Zeichen '.'
Zeichen ')'
Zeichen '"'           # Nur ein Zeichen auf dieser Taste.
Zeichen ','           # Only one symbol on this key.
Zeichen '('

```

To determine what your character set should be, you’ll need to determine what punctuation you type most frequently (which will depend upon your use case). I did this with a short Python script and a text corpus from exactly the sort of thing that will compose the majority of my non-code typing in the future: exegetical Bible studies. I downloaded all the major studies from [Ichthys.com](http://ichthys.com), the main Bible study site I follow, [in RTF form](http://ichthys.com/zip-msword.ZIP). I then converted them into plain text files, and counted character frequencies. (The Greek and Hebrew scripts were not converting well for some reason, so I just straight converted without bothering with Unicode — all the Greek and Hebrew words got replaced with question marks, which means that the character frequency of ? is somewhat higher than it should be).

[Here’s the Python script](https://steventammen.com/assets/files/keyboard-layouts/LetterFreq.py) I used to do this:

```
#-------------------------------------------------------------------------------
# Name:            LetterFreq.py
#
# Author:          Steven Tammen
#
# Email:           steven@steventammen.com
#
# Created:         01/08/2016
#
# Copyright:       No
#-------------------------------------------------------------------------------

from csv import *

#specifies names of plain text files to make a corpus
#for the frequency analysis. I was lazy and used relative
#references, but if you specify the paths unambiguously there
#is no reason why this script needs to be in the same
#directory as the files.
fileNames = (
    "1Theo.txt",
    "2A-Angelo.txt",
    "3A-Anthro.txt",
    "3B-Hamartio.txt",
    "4A-Christo.txt",
    "4B-Soterio.txt",
    "5-Pneumato.txt",
    "E1.txt",
    "E2.txt",
    "E3.txt",
    "E4.txt",
    "E5.txt",
    "E6.txt",
    "E7.txt",
    "Exodus-intro.txt",
    "Genesis-Questions.txt",
    "ICHTHYS-Acronym.txt",
    "intro.txt",
    "matthew-questions.txt",
    "Pet00.txt",
    "Pet01.txt",
    "Pet02.txt",
    "Pet03.txt",
    "Pet04.txt",
    "Pet05.txt",
    "Pet06.txt",
    "Pet07.txt",
    "Pet08.txt",
    "Pet09.txt",
    "Pet10.txt",
    "Pet11.txt",
    "Pet12.txt",
    "Pet13.txt",
    "Pet14.txt",
    "Pet15.txt",
    "Pet16.txt",
    "Pet17.txt",
    "Pet18.txt",
    "Pet19.txt",
    "Pet20.txt",
    "Pet21.txt",
    "Pet22.txt",
    "Pet23.txt",
    "Pet24.txt",
    "Pet25.txt",
    "Pet26.txt",
    "Pet27.txt",
    "Pet28.txt",
    "Pet29.txt",
    "Pet30.txt",
    "Pet31.txt",
    "readbible.txt",
    "Salvation.txt",
    "SR1.txt",
    "SR2.txt",
    "SR3.txt",
    "SR4.txt",
    "SR5.txt",
    "Tribulation-Part1.txt",
    "Tribulation-Part2A.txt",
    "Tribulation-Part2B.txt",
    "Tribulation-Part3A.txt",
    "Tribulation-Part3B.txt",
    "Tribulation-Part4.txt",
    "Tribulation-Part5.txt",
    "Tribulation-Part6.txt",
    "Tribulation-Part7.txt", )


#creates a dictionary (Python's version of a hash table) and
#populates it with characters and their frequencies in the corpus.
#We can get away using nested for loops here (O(n^2)) since this
#corpus is only a few hundred thousand lines. You could do it a
#more efficient way but it is less intuitive.
charDict={}
for name in fileNames:
    f = open(name, 'r')
    st = f.readline()
    while len(st) != 0:
        st = st.strip('\n')
        for i in range(len(st)):
            if (st[i]).isalpha():
                char = (st[i]).lower()
            elif st[i]=="-" and (st[i-1]).isdigit():
                char="v-"
            elif st[i]==":" and (st[i-1]).isdigit():
                char="v:"
            elif st[i]==";" and (st[i-1]).isdigit():
                char="v;"
            else:
                char=st[i]
            if char in charDict:
                charDict[char] += 1
            else:
                charDict[char] = 1
        st = f.readline()
    f.close()


#sorts the keys in order of descending frequency for each category of
#interest: letters, numbers, and punctuation/other. Spaces, tabs, carriage
#returns, etc. are ignored purposefully since they are not relevant to our
#analysis.
letters = []
numbers = []
others = []
keys = charDict.keys()
for key in keys:
    if key.isalpha():
        letters.append(key)
    elif key.isdigit():
        numbers.append(key)
    elif key.isspace():
        continue
    else:
        others.append(key)
            
letterPairs=((key, charDict[key]) for key in letters)
letterPairs=sorted(letterPairs, key = lambda x: x[1], reverse = True)

numberPairs=((key, charDict[key]) for key in numbers)
numberPairs=sorted(numberPairs, key = lambda x: x[1], reverse = True)

otherPairs=((key, charDict[key]) for key in others)
otherPairs=sorted(otherPairs, key = lambda x: x[1], reverse = True)


#prints the frequencies to a csv file for further analysis in Excel
#(or an equivalent spreadsheet program). Some cleaning up is necessary
#to incorporate characters like em dashes and smart quotes in the
#frequencies of more typical characters (hyphens and quotes, etc.).
f=open("LetterFreq.csv",'w', newline='')
csvWriter=writer(f)
for letterPair in letterPairs:
    csvWriter.writerow(letterPair)
csvWriter.writerow([])
for numberPair in numberPairs:
    csvWriter.writerow(numberPair)
csvWriter.writerow([])
for otherPair in otherPairs:
    csvWriter.writerow(otherPair)
f.close()

```

And [here is what it outputs](https://steventammen.com/assets/files/keyboard-layouts/LetterFreq.csv) given my corpus (your text editor will have to support Unicode to see everything properly):

```

e,803528
t,598843
o,495798
i,492051
a,464314
s,434196
n,433896
r,395252
h,380846
l,277050
d,230886
u,175152
c,173898
f,168673
m,139501
w,124651
p,124395
g,123719
y,102014
b,98846
v,82177
k,30190
j,19117
x,8767
z,4264
q,4086
é,32
ŕ,17
ü,6
á,2
ř,1
ö,1
í,1
č,1

1,44448
2,27492
3,15772
4,12982
5,9927
6,8950
0,7933
7,7484
8,7304
9,7117

",",81519
.,79721
v:,32737
),30797
(,29007
"""",25318
v;,14123
',12307
v-,10621
:,8614
],7951
[,7947
-,5668
?,5045
;,3151
“,2781
”,2759
–,2660
!,1033
*,773
’,773
/,624
#,399
‘,138
&,137
=,87
—,53
_,52
`,42
%,19
<,17
>,16
+,12
…,10
•,10
{,2
},2
|,1
·,1

```

Due to the nature of the particular corpus I chose (which has a lot of scripture references), I chose to separate out the semicolons, dashes, and colons associated with scripture references (demarcated above as v; v- and v:, respectively), since they will be handled separately with the numbers.

For the base layer, we are only interested in the top 6 punctuation characters. While some of the numbers have a higher frequency (at least in this corpus) than the punctuation characters, there are good reasons for keeping the numbers together, which will be discussed below. If you combine the opening and closing smartquotes with the total for normal quotes, the six most frequent non-letter and non-number characters, in order of descending frequency, are:

1. comma
2. period
3. double quotes
4. close parenthesis
5. open parenthesis
6. apostrophe

After these six come the colon, brackets, and so forth. These will appear on a different layer. The frequency differences are large enough that they are not likely to be due to statistical artifact. This order is markedly different from what the author of the MTGAP algorithm has come up with for prose ([see here](http://mtgap.bilfo.com/theory-of-letter-frequency.html)). He no doubt used a much larger overall corpus to generate his order, but due to to the similarity of my writing style to the author of the present corpus (for example, a tendency towards favoring complex multi-clause sentences over simple sentences, using lots of parenthetical clauses for explanatory purposes, enclosing new terms, words/phrases being discussed, and neologisms in double quotes, etc.), I feel confident in saying that the above order is a closer match to my particular writing style. If you want this exercise to be accurate *for you*, you will have to analyze your own writing and try to find a corpus that matches it well. Using pre-generated orders like those linked to works well if your writing is very normal -- I write more formally in "casual" discourse than almost everyone else I have met, and use much more complicated language and sentence structure than most people, so a "one size fits most" approach is a poor match *for me specifically*. As the saying goes, YMMV.



## Pre-optimization Considerations

Before you spend time optimizing the character layout of your keyboard, you need to first make sure that you have an ergonomic keyboard, and that your work environment is setup properly. Failing to account for these things (which are really more important), no matter how good your character layout ends up being, will put you at a much higher risk for RSI and CTS.

Optimizing the character layout of your keyboard without first dealing with your workstation ergonomics is like fixing a small leak in a ship while ignoring the gaping hole in the hull — any benefit you gain here will be vastly overshadowed by the gains from improving these other areas. Again, let me repeat myself, focusing on the character layout before settling these other matters is *not* wise, and I suggest you take some time to fix any deficiencies in your current equipment/habits before continuing.

## Reasons Why You Should Not Optimize

### Priorities

Please have a look at [this page](https://steventammen.com/priorities/).

Keyboard layout optimization must be taken as an investment of lower marginal benefit than many things before it. It is a worthy investment, but it is not the worthiest of your consideration unless several more important things have been taken care of beforehand.

I would encourage you to go through that link and make sure you have those things in good order before you even consider sinking in time on the keyboard optimization front. Also consider how much you really type in your everyday life (and thus how big a priority optimization is): programmers and secretaries, for example, type far more than park rangers or bakers, so keyboard optimization makes more sense for them.

### The Difficulty of Retraining Your Fingers

To put it simply, if you are already at 100 WPM typing QWERTY, and aren’t facing or likely to face RSI, you need to consider if this exercise is worth your while. Optimized layouts (even the bad ones, so to speak), are very much more efficient than QWERTY, and they drastically reduce the amount of effort it takes to type. But there will be an adjustment period of weeks not days, and recovering your old speed will take time. This goes doubly for those of you already using a better layout like Dvorak, Colemak, or Workman. I promise you that you can do better than any one of those three, but the gains will not be earth-shattering.

If the switch were easy or effortless, QWERTY would have ceased to exist long ago. As it is, however, you will be reduced to single digit WPMs for the first little bit, and your fingers will disobey you — you will have to rewire the neural connections in your brain that correspond to what we call “muscle memory.” If you have any sort of time-sensitive full-time occupation that forces you maintain your QWERTY skills (i.e., you can’t afford to go cold turkey and immerse yourself), it’s even harder because you’ll experience [proactive interference](https://en.wikipedia.org/wiki/Interference_theory#Proactive_interference) from already having QWERTY in muscle memory. That is to say, instead of “unlearning” QWERTY when you learn your other layout (replacing the old muscle memory with new muscle memory), the old muscle memory that you need to keep around will inhibit effective acquisition of the new muscle memory.

Depending on your dedication and consistency in practice, getting back to your previous speed can take anywhere from a few weeks to a few months. Poor discipline and lack of self-control can even push this from “difficult” to “impossible” — just like many people have tried to quit smoking and failed, many have tried switching away from QWERTY and failed. I would suggest that you not waste your time if you are not willing or able to put in the work necessary to be successful.

### QWERTY’s Ubiquitousness

As mentioned above, holding QWERTY in muscle memory when learning a new layout results in proactive interference. For most people, the flipside, called [retroactive interference](https://en.wikipedia.org/wiki/Interference_theory#Retroactive_interference), also holds true. Learning another layout will typically result in a loss of QWERTY speed because more errors are made — when you are trying to type a letter, your finger “forgets” that you are typing QWERTY, and instead presses the key for the letter on your other layout. While this is a problem for everyone, some people, through practice, have been able to keep high speeds on two different layouts simultaneously (e.g., Dvorak and QWERTY). Learning two layouts that are more similar to each other (like QWERTY and Colemak) is more likely to result in retroactive interference (just how learning Italian if you speak Spanish is more likely to mess with your Spanish than if you learn German), while using different physical keyboards for different character layouts (e.g., using Dvorak on a Kinesis Advantage and QWERTY on normal row-staggered keyboards) can help prevent retroactive interference.

The upshot of all this is that most people don’t continue to type with two different layouts in the long run — in other words, learning an optimized layout generally means you lose your QWERTY proficiency. The “problem” with this, of course, is that the rest of the world is designed for QWERTY and expects you to use it.

Not being able to touch-type QWERTY means your productivity will take a hit whenever you have to type on it for some reason (e.g., working on someone else’s computer or taking the GRE). You will also have to contend with poorly designed keyboard shortcuts (i.e., those with QWERTY in mind), which usually only prove to be problematic in those programs that don’t let you change them (boo on them). These are unavoidable consequences that you will face because QWERTY has become the expected layout in our society -- if you find them unacceptable, stick with QWERTY.

### The Animosity of Others

Certain people get rather worked up any time someone mentions a layout other than QWERTY. My best guess is that this is because the superior efficiency of people who type on other layouts is a direct challenge to their self-perception as competent, effective workers. It's also possible that their defensiveness is a manifestation of the [sunk cost fallacy](https://en.wikipedia.org/wiki/Sunk_cost#Loss_aversion_and_the_sunk_cost_fallacy): having spent a significant amount of time learning to touch-type QWERTY, they don't want to admit that they picked a bad layout. There is also likely a degree of [choice-supportive bias](https://en.wikipedia.org/wiki/Choice-supportive_bias): similar to how people evangelize the make and model of the new car they bought to help convince themselves it was worth it, people are more likely to evangelize QWERTY after deciding to make it their keyboard layout.

Whatever their motivations, people will frequently challenge your decision to use a layout other than QWERTY. If you are not the type of person that's cool taking heat for being different or constantly having to explain yourself, you may want to think twice about using a layout other than QWERTY.

(Note: you will encounter a larger group of people that is not actively antogonistic but merely confused as to why you find using another layout necessary or prudent. By and large, people in this group are happy shrugging and letting you do your thing if that's what you want -- but they may still give you weird looks. YMMV)

### Most Speed Considerations Are Layout Agnostic

There is a very real possibility if you switch that the time lost in getting back up to speed would have been better spent honing your mastery of whatever layout you do currently use, because most of the ways you can accelerate your typing don’t depend on your layout. In other words, it may very well be better for you to spend a couple months increasing your QWERTY speed from 60 WPM to 100 WPM than getting up to 60 WPM on another layout.

#### Practice

There is no magic here. Optimizing your layout won’t immediately make you a faster typist, though it certainly has the potential to eventually. The thing that will make you a faster typist is practicing a layout until you breathe it and you dream about it. This is like every single other skill in existence; the more you practice, the better you get. 

I want to here emphasize that not all practice is equal. Practice does not make perfect. Practice makes permanent (or, alternatively, “perfect practice makes perfect”). Because we tend to type a great deal in our day to day lives, there is a danger of just going on autopilot and plateauing. Whether or not you decide to continue on in this process, I can recommend that you pick up typing not as something one merely does, but as something one studies and perfects over time.

Practice the most common digraphs and trigraphs in English (or your native language if not English). Lists can be found [here](http://scottbryce.com/cryptograms/stats.htm), [here](http://www.cse.unt.edu/~mgomathi/teaching/2009/csce5550/Lectures/Cipher-Example%202.pdf), and elsewhere through a simple Google search. If you consciously train yourself to type *sequences* rather than *letters*, your speed will increase at a much faster rate.

To extend this concept even further, you should drill with [this repo](https://github.com/first20hours/google-10000-english), which has the 10,000 most common words in English. It does you little good to type uncommon or unusual words at a high speed because they compose a small portion of what you type (e.g., typing “zyzzyva” fast does you no good because genuses of weevils don’t come up in normal conversation). Getting very fast at words like “the”, “and”, “that” and so forth, however, will dramatically increase your speed because these words compose a large percentage of everything we type.

#### Text Expansion

If you really want to ramp up the speed, you should use text expansion to abbreviate at least the first couple hundred most common words and phrases in English, making, for example, “the” just “t”, “I want to” just “iwt”, and so on. By doing this alone, you can cut down on how many keys you have to physically press down by a huge percentage (at least for prose). You can actually do the same thing for common code constructs (e.g., the basic syntax of a for loop in Python), email signatures, and really anything else you can think of. Since I’m on Windows, I personally use AutoHotkey for this purpose, but there are plenty of options for this sort of thing. If your keyboard supports it, you may be able to do text expansion on the firmware level, making it operating system and device agnostic.

Just like normal typing, you’ll need to practice this intentionally to get results, retraining your hands to type “t” every time your brain thinks “the”. You’ll also want to create a “theory” for your abbreviations, and come up with some patterns to reuse as your list grows (e.g., using consistent letter sequences for phrase enders — “iwt” for “I want to”, “hwt” for “he wants to”, “swt” for “she wants to”, etc.). A working knowledge of a brief-heavy stenographic theory will help you here.

#### Modal Text Editing

Whether you code or not, you should consider learning [Vim](http://www.vim.org/) bindings and modal text editing. While I explicitly optimized for some of Vim’s bindings (more on the reasoning for that later — specifically why I chose to attach myself to the Vim framework instead of building my own syntax from the ground up), learning them on any layout is much, much, better than being stuck in the land of GUIs and text editing by mouse. Vim happens to be very well laid out for QWERTY since it was designed for QWERTY, but other layouts like Colemak can easily adapt to it as well.

In terms of implementing this, I would suggest you not pick up vanilla Vim or gVim, but rather [Spacemacs](http://spacemacs.org/) (which uses Emacs’ evil mode to emulate Vim commands) or [NeoVim](https://neovim.io/) (which improves on many of Vim's strengths and brings it into the 21st century).

Because of [Org Mode](http://orgmode.org/), its support for non-leader key remapping of commands, and mnemonic key sequences for specialized commands (such as window commands), I personally believe Spacemacs is the superior choice for most people and situations. However, many others like [NeoVim](https://neovim.io/) combined with [Tmux](https://github.com/tmux/tmux) and [Zsh](http://www.zsh.org/). In my opinion, the decision between these two setups mostly comes down to how much you use Org Mode -- since I use Org Mode for basically everything that's not code, I use Spacemacs.

#### Symbol Layers

You can create layers for numbers and symbols (putting them on the home row or at least in favorable positions) while still using QWERTY for letters. These additional layers have nothing to do with letter layouts.

#### Conclusion

Most speed considerations are layout agnostic. If you are already a sufficiently fast typist with another layout, the opportunity cost of retraining may be better spent beefing up your current toolkit and optimizing other parts of your typing. No matter what you do, dedicated *intentional* practice can significantly improve your typing, and you shouldn’t switch without first considering if it is really the most rational decision under your circumstances. For the reasons why you *should* switch, read on.

## Reasons Why You Should Optimize

### Reduced Typing Effort

Far and away the biggest benefit optimized keyboard layouts give is a greatly reduced overall typing effort. As will be discussed below, optimized layouts significantly reduce the amount of distance your fingers need to travel by putting frequently used keys in favorable positions (like the home row), and balance finger and hand distribution so that effort is spread out. They also strive to make frequent two-letter combinations (called digraphs) and three-letter combinations (called trigraphs) easy to type: he, th, tha, str, and so forth.

It is perhaps easiest to demonstrate the benefits of optimized layouts by counterexample: using "problem words" from QWERTY.

1. On QWERTY try typing the word "stewardesses." It should be immediately obvious what the problem here is: your left hand does all the work while your right hand just sits there doing nothing!
2. Now try typing the word "minimum." Aside from being another example of one hand doing all the work, QWERTY's minimum has additional problems: you have to jump over the home row to get from M and N to I and U, and you have to use the same finger to type M and U in succession. As variables, these are usually called "row jumping" and "same-finger", respectively, and most optimized layouts try to minimize them as much as possible.

Basically, optimized layouts have less words like QWERTY's "stewardesses" and "minimum" -- words that are hard to type, split the load unequally among fingers and/or hands, require your fingers to travel further, etc. Consequently, typing is less effortful on optimized layouts.

### Reduced Repetitive Stress Injury (RSI)

Theoretically, the reduced overall effort needed to type on an optimized layout could lead to a delay in onset and/or remission of symptoms for those suffering from RSI, but there currently isn't a great deal of statistically useful data out there (though anecdotal success stories abound, they are not verifiable, and may be demonstrating the power of the placebo effect rather than the power of optimized keyboard layouts). On the other hand, it would make sense if less effort over time led to less "repretitive stress" overall (even if science hasn't verified this yet), so giving it a shot may still be worth it.

It is once more worth pointing out that a good keyboard and proper workstation ergonomics are much more important than a character layout ever will be on this front, so if you don't have these things in order, an optimized keyboard layout won't save you from RSI.

### Increased Typing Speed

While this is perhaps the most controversial of the benefits (and is yet to be verified in a rigorous way, like RSI reduction above), there is a theoretical basis for faster typing on optimized layouts. For example:

- Optimized layouts require less overall finger travel distance, with most of the most frequent letters and combinations requiring no movement from the home row. Less required movement ought to lead to faster speeds, all other things being equal.
- Optimized layouts have higher hand alternation than QWERTY. Hand alternation makes it easier to line up the next letter when typing the previous one, since your fingers on the next-letter hand will not be out of position from typing letters on the top or bottom rows. (Cf. the QWERTY digraphs "he" and "in". For the former -- an example of hand alternation -- E can easily be lined up while you are pressing the H key since they are on different hands despite being on different rows. For the latter, it is harder to line up N when you are pressing I since I is on the top row of the right hand and N is on the bottom row of the right hand). This too should theoretically lead to faster speeds.
- Optimized layouts have less same-finger (as in QWERTY "fr" or "ed"). It is not possible to line up subsequent letters in any way for same-finger digraphs, making them the slowest letter combinations. It follows then that layouts with less same-finger combinations will enable faster typing.

I'm sure there are other such features that could be mentioned in support of optimized layouts being faster (i.e., this list is not intended to be comprehensive); however, until rigorous studies are done, all of this is theoretical. The effects mentioned above are going to be much less significant than practice overall -- which is why some QWERTY typists like [Sean Wrona](https://www.youtube.com/watch?v=4GDusA21cEA) will destroy the vast majority of people who type on optimized layouts.

## Outline of Optimization

### Introduction and Explanation of Methodology

I have, in some form or another, been working on optimizing my keyboard layout for a couple years now. This is not to say I've spent a great deal of total time on it, or that you should automatically listen to me. There are plenty people much smarter than I who have worked on the problem and come up with different solutions. But I hope by documenting the process it might be made less mysterious overall, especially for people who haven't ever compiled C++ code from a shell instance and think that a genetic algorithm is something related to DNA.

In this section I will first go over each of the relevant factors in optimization, then discuss how we ought to go about weighting them (which is really the tricky part). Finally, I will go over some of the preliminary design considerations that must be taken into account when designing a layout.

- Optimization Considerations
   - Differences in Hand Morphology
      - My Hand Morphology
   - Differences in Optimization Goals (speed vs ergonomics)
      - My Optimization Goals (balance)
   - Differences in Textual Corpus
      - My Textual Corpus (Latin, Greek, Hebrew, German, French, Italian, Spanish, Markdown, Org, LaTeX, programming, number entry)
   - The Unavoidability of Opportunity Cost: Coming to an “Optimal Compromise”
   - The Danger of Perfectionism
- Character Layout Design Factors
   - Finger Travel Distance
   - Same Finger
   - Indirect Same Finger
   - Shift Same Finger
   - Hand Alternation
   - Two Hand Alternation
   - Inward Motion Frequency
   - Outward Motion Frequency
   - Inward/Outward Motion Ratio
   - Inward Roll Frequency
   - Outward Roll Frequency
   - Inward/Outward Roll Ratio
   - Roll Conformity to Standards Based Upon Hand Physiology and Subjective Analysis
   - Vertical Hand Shift (“Row Jumping”)
   - Number of Movements Between Rows
   - Horizontal Hand Shift (“Column Jumping”)
   - Number of Movements Between Columns
   - Finger Load Conformity to Standards Based on Hand Physiology and Subjective Analysis
   - Hand Balance
   - Adjacency
   - Shift Adjacency
   - Home Position %
   - Favorable Position %
   - Index Extension %
   - Pinky Extension %
- Weighting of Character Layout Design Variables
   - Comparison Methods
      - Layouts: Numerical Scores Based on Percentage-Based Weighting of Variables
      - Individual Factors: Percent Difference Between Layouts
      - Individual Factors: Normalization by Best Performing Layout
   - General Approaches: Specialization vs. Jack of All Trades
      - Imperfect Knowledge of Variable Importance in General
      - Imperfect Knowledge of Variable Importance with Respect to Individual Differences
- Preliminary Design Considerations
   - Additional Keys vs. Layers
   - The Most Efficient Methods of Accessing Layers: Leader Keys vs. Modifier Keys
   - The Most Efficient Keys to Access Layers: Thumb Keys vs. Finger Keys
   - Key Priority for a simple 40-Key Layout
   - Key Priority for a Multilayer 40-Key Layout
   - Subjective Key Weighting for a simple 40-Key Layout
   - Subjective Key Weighting for a Multilayer 40-Key Layout
   - Dual Use: Modifiers on the Home Row
   - Key Scope: Usage Context Driving Availability
      - Importance
      - The Accessibility of Control Keys Across Layers
      - The Accessibility of Modifier Keys Across Layers
      - Space
      - Esc
   - Key Clustering Patterns
      - Importance
      - Numbers
      - Navigation/Editing
      - Mousing
   - Grouping and Consistency: Why Computer Optimized Layouts May Not Always Be Superior
      - A Brief Discussion of Human Cognition
      - “Chunking”
      - Key Frequency Considerations
- Base Layer
   - Reasons for Including All the Letters on the Base Layer
   - Reasons for Keeping E off of the Thumbs
   - A Comparison of Letter Layers
      - HIEAM as Superior Choice
   - Determining Which Punctuation Keys Should Go on the Base Layer
   - Determining How to Lay Out the Punctuation Keys on the Base Layer
   - Placement of the Space Key
   - Placement and Usage of the Shift Key
   - Using , for Entering Navigation/Editing Mode
      - {,} Alone Toggles on Navigation/Editing Mode
      - {,}{Spc} Acts as Normal
      - {, down}{Spc}{, up} Enters Vim Normal Mode With Spacemacs Leader Key Toggled
   - Using ) for Entering Commands
      - {)} Alone Focuses Command Box
      - Command structure: {)}{letters/numbers}{Spc/Enter/Tab etc.}
      - {)}{Spc} Acts as Normal
   - Using . for Entering Greek/Hebrew/etc. Mode
      - Either Greek or Hebrew is active mode: switch with ) commands
      - {.} Alone Toggles on Greek/Hebrew Mode (Whichever is active)
      - {.}{Spc} Acts as Normal
      - Hbr and grk hotstrings (hbr —> “Hebrew: ”) activate respective mode: used when listing what a word is in both languages regardless of current active mode on . key
- TODO Explain Nav Layer
- TODO Explain Greek Layer
- TODO Explain Shift Layers
- TODO Explain Number Layers
- TODO Explain Code Layer
- TODO Explain Symbol Layer
- TODO Explain Function Layer
- TODO Explain Media Layer
- Caveats
   - Character frequencies based on typing out all words; do not take into account text expansion/briefs
   - Writing Corpuses Change Over Time
   - Individual Physiological Factors Change Over Time (e.g., Arthritis)

## Punctuation results from ADNW Optimizer Evaluation

```

HIEAM            278.108 total effort   189.249 positional effort    left right
                   1.118 same finger rp  19.943 shift same finger top 12.9 13.4
  byou' kdclpq    70.243 hand alternat.  26.526 shift hand alter. mid 32.3 31.0
  hiea. mtsrnv     3.240 inward/outward  26.086 inward or outward bot  3.5  6.9
  x)",( wgfjz     10.621 adjacent         9.099 shift adjacent    sum 48.7 51.3
       ┬á           4.421 no hand altern. 43.359 two hand altern.
                   2.661 seesaw           6.645 indir same finger
                  8.2  8.6 18.9 13.0 --.- --.- 19.0 11.5  9.9 10.8 Sh  1.8  1.0


CommaMid         278.146 total effort   189.254 positional effort    left right
                   1.118 same finger rp  19.943 shift same finger top 12.9 13.4
  byou' kdclpq    70.243 hand alternat.  26.526 shift hand alter. mid 32.3 31.0
  hiea, mtsrnv     3.240 inward/outward  26.086 inward or outward bot  3.5  6.9
  x)".( wgfjz     10.621 adjacent         9.099 shift adjacent    sum 48.7 51.3
       ┬á           4.421 no hand altern. 43.359 two hand altern.
                   2.661 seesaw           6.645 indir same finger
                  8.2  8.6 18.9 13.0 --.- --.- 19.0 11.5  9.9 10.8 Sh  1.8  1.0


ParensPreferred  279.941 total effort   189.530 positional effort    left right
                   1.242 same finger rp  19.943 shift same finger top 12.9 13.4
  byou' kdclpq    70.243 hand alternat.  26.526 shift hand alter. mid 32.3 31.0
  hiea. mtsrnv     3.310 inward/outward  25.962 inward or outward bot  3.5  6.9
  x()," wgfjz     10.502 adjacent         9.082 shift adjacent    sum 48.7 51.3
       ┬á           4.421 no hand altern. 43.359 two hand altern.
                   2.609 seesaw           6.627 indir same finger
                  8.2  8.6 18.6 13.3 --.- --.- 19.0 11.5  9.9 10.8 Sh  1.8  1.0


ParensPreferred2 279.945 total effort   189.530 positional effort    left right
                   1.242 same finger rp  19.943 shift same finger top 12.9 13.4
  byou' kdclpq    70.243 hand alternat.  26.526 shift hand alter. mid 32.3 31.0
  hiea. mtsrnv     3.308 inward/outward  25.963 inward or outward bot  3.5  6.9
  x)(," wgfjz     10.492 adjacent         9.099 shift adjacent    sum 48.7 51.3
       ┬á           4.421 no hand altern. 43.359 two hand altern.
                   2.610 seesaw           6.626 indir same finger
                  8.2  8.6 18.6 13.3 --.- --.- 19.0 11.5  9.9 10.8 Sh  1.8  1.0


PeriodBot        286.922 total effort   192.021 positional effort    left right
                   1.308 same finger rp  19.943 shift same finger top 12.9 13.4
  byou' kdclpq    70.243 hand alternat.  26.526 shift hand alter. mid 31.4 31.0
  hiea" mtsrnv     3.256 inward/outward  25.897 inward or outward bot  4.4  6.9
  x).,( wgfjz     10.539 adjacent         9.099 shift adjacent    sum 48.7 51.3
       ┬á           4.421 no hand altern. 43.359 two hand altern.
                   2.627 seesaw           6.958 indir same finger
                  8.2  8.6 19.8 12.1 --.- --.- 19.0 11.5  9.9 10.8 Sh  1.8  1.0


SwapApos         281.110 total effort   189.254 positional effort    left right
                   1.246 same finger rp  19.943 shift same finger top 12.9 13.4
  byou" kdclpq    70.243 hand alternat.  26.526 shift hand alter. mid 32.3 31.0
  hiea. mtsrnv     3.282 inward/outward  25.958 inward or outward bot  3.5  6.9
  x)',( wgfjz     10.535 adjacent         9.099 shift adjacent    sum 48.7 51.3
       ┬á           4.421 no hand altern. 43.359 two hand altern.
                   2.629 seesaw           6.699 indir same finger
                  8.2  8.6 18.9 13.0 --.- --.- 19.0 11.5  9.9 10.8 Sh  1.8  1.0
                  
```

## Unorganized Thoughts

### Tap vs. hold:

- For the sake of easy numbers, let’s assume a few things:
   - Selecting a key to press takes 0.25 seconds (the decisionmaking time to press this key instead of that key )
      - The decisionmaking time for a second down movement of a key will be less, assuming the presses are next to each other in the key-stream (i.e., aa or aba instead of abca or abcda). Presses directly contiguous take between 0 and 0.125 seconds rather than normal 0.25; presses indirectly contiguous take between 0.125 and 0.25 seconds. These reductions are due to the fact that the cognitive load of this second press is less than acquiring an entirely different key to press.
   - The decisionmaking process for pressing down another key begins as soon as the down movement for the prior key begins, or, in the case of a key getting pressed for a second time, as soon as the first up movement is completed, or, in the case of same finger, as soon as the up movement of the first key is completed.
   - each down movement takes 0.25 seconds to complete 
      - Deciding to release a key takes 0 seconds if done immediately after pressing it, and between 0 and 0.125 seconds if not done immediately after pressing it.
   - Each up movement takes 0.25 seconds to complete
   - For cases of same finger, it takes between 0.125 and 0.25 seconds to move the finger in question from one location to another

### TODO: add Excel Results Table

### Available double-tap triggers:

- code code
- sym sym
- yy
- jj
- xx
- qq

### Available double-tap triggers when not in code mode:
- ((
- ‘’

Not in code mode: keyboard/program keeps track if inside unclosed quotes, “ key will then use single quote to automatically nest (allows us to use ‘ key in accents). “” —> “‘

Redesign Vim modal editing by matching most frequent commands to most frequent letters/symbols, assuming that these letters will be placed in favorable positions on kb layouts, making the vim bindings (relatively) layout independent. < Job for more dedicated/full-time person

Placement of sym layer with right thumb because sym will not be prepended/followed by numbers which require right thumb while code can be (e.g., [1, 2, 3] or 5>3). Assuming accessing shift layer not much difference between code and sym layers.

Command keys (Enter, Tab, Bkspc, Del) go on outer pinkies because don’t want to press them accidentally, not used in rolls/key combinations. Enter goes opposite punctuation. Also frequency considerations.

Punctuation always followed by space/enter can go on shift layer off home row since won’t mess with same finger for most circumstances (: used as punc goes here — used as leader, accessed on number layer — typical disadvantages from holding down don’t apply with thumb key never followed by space). - also goes here so it can be accessed by leader in a home position instead of only accessible by hold-down on middle finger extension. Esc on this layer too.

/ on left due to URLS: more words starting/ending with consonants than vowels (?)

## Other Languages: Goal

To be able to type Latin, German, French, Italian, and Spanish on the normal English layer without dead keys or other complicated methods of character entry and without interfering with Markdown, Org, or LaTeX markup syntax. As much as allowable by optimization constraints, the characters should be easy to memorize (:e —> ë rather than ^e —> ë) and consistent (if ]e —> œ, then it would make sense to use ]a —> æ; pattern: ] + letter —> ligature).

### Character priority:

- ,{letter}
- .{letter}
- ){letter}
- {letter}(
- ‘{letter}
- :{letter}  =  {letter}\`
- characters on non-thumb keys on Code and Sym layers, prioritized by memorability (see below)

Can’t use $ (thumb key > other fingers) since it is used in LaTeX for the inline/display modes of mathematical expressions. (It would be possible to track the opening/closing similar to \` code blocks in MD, but in some circumstances you might want to retain the ability to write accents within an expression.)

Thus far in my layout, ,{letter} is being used to jump into the navigation layer/toggle normal mode in Vim, .{letter} is being used to jump into Greek/Hebrew mode, and ){letter} is being used in command mode. The navigation and command modes are obviously more important than diacritics, and for me the Greek/Hebrew mode is more important as well since I type these languages more frequently than non-English languages with the Latin alphabet (including Latin itself). YMMV

### Memorability considerations:
- \| looks like a macron
- ( looks like a breve or inverted breve
- ) looks like a breve or inverted breve
- { looks kind of like a caron
- } looks kind of like a caron
- : looks like an umlaut/a dieresis
- A typographically smartened ‘ in the middle of a word looks like an acute accent (ex’ample)
- \` looks like a grave accent
- ^ looks like a circumflex accent for Latin scripts (the Greek/Cyrillic circumflex is a tilde accent or inverted breve) or inverted caron
- ~ looks like a tilde accent/the top part of the Spanish letter eñe (ñ)
- The Spanish letter eñe (ñ) looks like n
- , looks like the tail used to form a French c-cedilla (ç), a Romanian t-comma (ț), and a Romanian s-comma (ș).
- A c-cedilla (ç) looks like c, a t-comma (ț) looks like t, and an s-comma (ș) looks like s.
- The German ß is phonetically similar to s, but looks kind of like a capital B
- / looks like the slash in the Norwegian/Danish ø
- \ looks like the slash in the Norwegian/Danish ø, except facing the wrong way
- 0 looks like the circle above the Norwegian/Danish/Swedish å
- The Spanish inverted question mark (¿) looks like ?
- The Spanish inverted exclamation mark (¡) looks like !

### Accents

(in order of frequency: Latin > German, French, Italian > Spanish; presupposing prose mode not code mode; organized by decreasing freq. below)

- macron
   - o(
   - ( never used after letter
- acute accent
   - ‘o
   - ‘ only used before t, s, ve
- umlaut/dieresis
   - :o
   - : never used before letter
- grave accent
   - o\`
   - \` after resets hand for next, code
- circumflex
   - ^o
   - ^ before follows superscript ^{}

Track open \`code blocks\` (markdown) similar to open “. Code mode activated (and hence accents disabled, including grave) in open code blocks.

Brackets are not used with numerical superscripts (e.g., 1.2 x 10^8) in normal use. However, when the superscript is text, brackets become necessary to eliminate ambiguity: this^superscripted text vs. this^{superscripted text}. Thus, ^ before will never cause conflicts since text based superscripts will always use brackets.

No breve is needed since the absence of a macron indicates a short syllable.

### Letters and Ligatures 

(in order of frequency: Latin > German, French, Italian > Spanish; presupposing prose mode not code mode)

German

- ß eszett
   - s(
   - ( >> ‘ for these: ‘s, bot diag>top

French

- ç c-cedilla
   - c(
- œ oe ligature
   - ]e
   - ] before rather than [ after avoids SF
- æ ae ligature
   - ]a 

Spanish

- ñ eñe
   - n(
- ¿ inverted ?
   - ?{letter}
- ¡ inverted !
   - !{letter}

You should customize the typing of diacritics for your use case by looking at character frequency. Since most folks have no use for an automatic layer for Greek/Hebrew and also don’t need macrons, .{letter} and {letter}( should be used for different things.

## Hotstrings/Briefs

KB Briefing: Python script, top 100 or 200 words by freq in english language, use csv file to list word and possible briefs, check possible briefs against Spanish/French/Italian/German/Latin words, use script to match up (non-conflicting) possible briefs to the words that lead to the maximum amount of typing saved.

## AHK Dual Script Modding

- Sending key combinations in combinators
- Being able to easily toggle how Dual sends keys (send-mode input vs send-mode event).
- Making it easy to make all keys (even those that are not dual role keys) send their character on key-up rather than key-down. Consistency would make the “lag effect” (which lessens the faster you go) much easier to bear at slower speeds.
- Figure out non-base-layer hotstrings. Also figure out how to send key combinations in key sequences (e.g., Ctrl+Bkspc, Ctrl+Del).
- Hotstrings for “. o” —> O etc. (auto-capitalize first words of sentences)? Do with foreign letters too?
- Make shift work with macroned letters etc.
- Alt lock (for unicode symbols)?

