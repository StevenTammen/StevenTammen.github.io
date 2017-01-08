---
permalink: /keyboard-layouts/hieam/
layout: layout
title: HIEAM
---

<div class="center">

   <h1>The HIEAM Layout</h1>
   
   <a href="https://github.com/StevenTammen/steventammen.github.io/edit/master/pages/keyboard-layouts/hieam.md" target="_blank">
     <img src="https://steventammen.github.io/assets/images/GitHub.png" height="30" width="30">
   </a> &nbsp; &nbsp;
   
   <a href="http://prose.io/#StevenTammen/steventammen.github.io/edit/master/pages/keyboard-layouts/hieam.md" target="_blank">
     <img src="https://steventammen.github.io/assets/images/Prose.png" height="30" width="30">
   </a>
   
</div>

## Outline

- Explanation of Methodology
- Optimization Considerations
   - Differences in Hand Morphology
      - My Hand Morphology
   - Differences in Optimization Goals (speed vs ergonomics)
      - My Optimization Goals (balance)
   - Differences in Textual Corpus
      - My Textual Corpus (Lat, Grk, Heb, Grmn, French, Italian, Spanish, theological writing, Markdown, Org, LaTeX, programming, number entry)
   - The Unavoidability of Opportunity Cost: Coming to an “Optimal Compromise”
   - The Danger of Perfectionism
- Physical Layout Design Variables
   - Why Physical Layout Design Must Come First
   - Design Philosophy: Everything is a Variable
   - Comfort/Ergonomics
      - Split-Hand Design
      - Columnar Key Layout
      - Adjustable Wrist Pronation (“Roll”)
      - Adjustable Elbow Angle (“Yaw”)
      - Adjustable Typing Angle (“Pitch”)
      - Neutral Position Wrist Wrests
      - Column Stagger
      - Key Height Differentials
      - Concave Keywells
      - Keyswitch Actuation Force
      - Keyswitch Travel Distance
      - Keycap Shaping
   - Typing Speed
      - Concave Keywells
      - Keyswitch Actuation Force
      - Keyswitch Travel Distance
      - Keycap Shaping
   - Portability
      - Wired/Wireless/Bluetooth Capability
      - Combination Mechanism
      - Combined Keyboard Fragility
      - Combined Keyboard Length
      - Combined Keyboard Width
      - Combined Keyboard Height
      - Combined Keyboard Weight
      - Traction On Different Surfaces
   - Durability/Ease of Maintenance
      - Keycap Material
      - Case Material
      - Key Grid Construction (Hand-Wired vs. PCB)
      - Keyswitch Stem Type
      - Replaceable Connection Mechanism Between Keyboard Halves
      - Replaceable Connection Mechanism To Computer
   - Functionality
      - Keyboard Microcontroller
      - Key Backlighting
      - Signalling Mechanism For Mode Lock Engagement (e.g., CapsLock, NumLock)
      - Toggleable Noise For Key Actuation
- Weighting of Physical Layout Design Factors
   - Identifying Which Factor Group Is Most Important For You
   - Portability: The Relationship Between Familiarity And Speed
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
   - Using . for Entering Greek/Hebrew Mode
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
- TODO Explain Mouse Layer
- TODO Explain Function Layer
- TODO Explain Media Layer
- Caveats
   - Character frequencies based on typing out all words; do not take into account text expansion/briefs
   - Writing Corpuses Change Over Time
   - Individual Physiological Factors Change Over Time (e.g., Arthritis)


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
- - ‘{letter}
- :{letter}  =  {letter}\`
- characters on non-thumb keys on Code and Sym layers, prioritized by memorability (see below)

Can’t use $ (thumb key > other fingers) since it is used in LaTeX for the inline/display modes of mathematical expressions. (It would be possible to track the opening/closing similar to \` code blocks in MD, but in some circumstances you might want to retain the ability to write accents within an expression.)

Thus far in my layout, ,{letter} is being used to jump into the navigation layer/toggle normal mode in Vim, .{letter} is being used to jump into Greek/Hebrew mode, and ){letter} is being used in command mode. The navigation and command modes are obviously more important than diacritics, and for me the Greek/Hebrew mode is more important as well since I type these languages more frequently than non-English languages with the Latin alphabet (including Latin itself). YMMV

### Memorability considerations:
- | looks like a macron
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

macron			o(	( never used after letter
acute accent		‘o	‘ only used before t, s, ve
umlaut/dieresis	:o	: never used before letter
grave accent		o`	` after resets hand for next, code
circumflex		^o	^ before follows superscript ^{}

Track open \`code blocks\` (markdown) similar to open “. Code mode activated (and hence accents disabled, including grave) in open code blocks.

Brackets are not used with numerical superscripts (e.g., 1.2 x 10^8) in normal use. However, when the superscript is text, brackets become necessary to eliminate ambiguity: this^superscripted text vs. this^{superscripted text}. Thus, ^ before will never cause conflicts since text based superscripts will always use brackets.

No breve is needed since the absence of a macron indicates a short syllable.

### Letters and Ligatures 

(in order of frequency: Latin > German, French, Italian > Spanish; presupposing prose mode not code mode)

German
ß eszett			s(	( >> ‘ for these: ‘s, bot diag>top

French
ç c-cedilla		c(
œ oe ligature		]e ] before rather than [ after avoids SF
æ ae ligature		]a 

Spanish
ñ eñe			n(
¿ inverted ?		?{letter}
¡ inverted !		!{letter}

You should customize the typing of diacritics for your use case by looking at character frequency. Since most folks have no use for an automatic layer for Greek/Hebrew and also don’t need macrons, .{letter} and {letter}( should be used for different things.
