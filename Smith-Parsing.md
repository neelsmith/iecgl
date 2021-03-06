---
author: Neel Smith
title: Parsing Greek morphology
date: ICGLE, August 29, 2017
header-includes:
    - \setsansfont{Gentium}
---

# ... in multiple dialects and alphabets

-   local dialects
-   epichoric scripts

---



# Digital scholarship and Classics


-   25 years ago: a leading discipline
-   today: largely absent from new areas of textual analysis?


---


# Example: latent pattern recognition

-    topic modelling
-    semantic relations with embedded word vectors

---

# Some reasons, good and bad

-   disciplinary culture?
-   corpus size vs. tolerance for imprecise editions
-   **morphological complexity**


---

# Motivation

Homer Multitext project: manuscripts with

-   multiple dialects
-   unattested vocabulary
-   distinct orthographies

![The Venetus A manuscript](imgs/VA012RN-0013.jpg)

---

# Current standards


-   ISO 639* family: Greek dialects not recognized
-   Unicode:
    -   language and script conflated
    -   epichoric scripts not recognized
    -   confusion of multivalent and contradictory glyphs

---



![Peter Bruegel the Elder, 1563, KHM GG 1026](imgs/babel.png)



---


> In 2017, it is (still!) not possible to encode Greek


---



![A Vienna secession?](imgs/secession.png)


---


# Secession, 1: orthography

>**not** "the" Greek alphabet, but multiple systems
> for writing Greek

---


# Specifying an orthography


-   encoding in (primarily) ASCII characters with distinct character for accent, breathing
-   encoding in (primarily) Greek Unicode suitable for display


---

# Encoding Greek

Literary Greek:


>ἔδοξε == e)/doce

Pure diplomatic rendering of classical Attic:

>εδοχσεν == EDOXSEN

Editorially normalized version of classical Attic:

>ἔδοχσεν τêι βολêι == E)/DOXSEN TE=I BOLE=I

---

# Secession, 2: language

>**not** "Greek," but the Greek of a specific corpus
>


---

# A corpus-linguistic perspective

-   For historical languages, every analysis is corpus-specific
-   Every corpus is characterized by:
    -    a unique **lexicon** in a specified orthography
    -    a unique set of **inflectional** rules in a specified orthography

---

# So not *a parser*, but...

>a system for building corpus-specific parsers




---


# Citable results

-   each lexicon entry has a unique ID for *lexical entity*
-   each *inflectional rule* has a unique ID


---

# An analysis is composed of

1.   a string of characters analyzed
2.   a specified form
3.   a uniquely identified lexical entity
4.   a uniquely identified inflectional rule


---

# "Greek" is defined by *values specifying form*


- "noun" (GCN)
- "adjective" (GCND)
- "conjugated verb" (PNTMV)
- "infinitive" (TV)
- "participle" (GCTMV)
- "verbal adjective" (GCN)
- "adverb" (degree)
- "indeclinable" (part of speech)





---

# Kanónes

(*not* Theodosius of Alexandria!)

A system for building parsers from tables by defining:

1.  inflectional rules
2.  a lexicon of "stems"



---

# Parsing morphology

-   standard technology: **finite state transducers** (FST)
-   require context-free state transitions

---

# Parsing Greek


FSTs fail!

>Accent crosses lexical and inflectional properties
>
>->  cannot be reduced to context-free state transitions

---


# Solution in Kanónes


"Analysis by synthesis" algorithm:


1. collect an accented word
2. strip its accents, and use FST to get *possible* analyses
3. algorithmically apply correct accent
4. compare accented candidate forms to original word

---

# Example parse

1. original word: **εἶπε**
2. εἰπε analyzed as:
    - 3rd singular aorist indicative active
    - 2nd singular aorist imperative active
3. accenting yields:
    - εἶπε for 3rd singular aorist indicative active
    - εἰπέ for 2nd singular aorist imperative active
4. so solution is **3rd singular aorist indicative active**




---

# A simple worked example: two parallel corpora

---


Andocides *On the Mysteries* 1.96

> Νόμος. ἔδοξε τῇ βουλῇ καὶ τῷ δήμῳ.

---

IG 1.3, 156

![Decree honoring Leonides of Halicarnassus](imgs/decree-masked.png)


---

# Vocabulary ("stems")

![Nouns, in Attic](imgs/attic-noun-stems.png)

![Nouns, in literary Greek](imgs/lit-noun-stems.png)

---

# Inflectional rules

![Nouns, in Attic](imgs/attic-noun-infl.png)

![Nouns, in literary Greek](imgs/lit-noun-infl.png)

---

# Analysis

![literary Greek](imgs/analysis-lit.png)

---


# Analysis

![Attic Greek](imgs/analysis-attic.png)




---


# Generated


![literary Greek](imgs/generator.png)

---

# Pipeline

Output of Attic analysis -> literary Greek generator


![From Attic to literary Greek](imgs/pipeline.png)

---

# Current state


-   largely completed in 2016 using Stuttgart FST toolkit + Java/Groovy custom classes
-   summer 2017:  porting custom classes to Scala substantially complete
-   initial test corpora from HMT project:
    - complete *Iliad* manuscripts
    - more than 10,000 scholia


---

# Possibilities


-   morphologically sensitive structured searching
-   lexically unified corpus for latent pattern analysis
-   integration of corpora in distinct writing systems or dialects
-   pedagogy with epigraphic material in distinct writing systems or dialects?


---

# Thank you!

For more information:

-   "Morphological Analysis of Historical Languages," *BICS* 59-2 (2016) 89-102.
-   <https://github.com/neelsmith/kanones>
