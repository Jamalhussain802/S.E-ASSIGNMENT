# Behind the Intents: An In-depth Empirical Study on Software Refactoring in Modern Code Review


# Authors:

# Matheus Paixao , 

# Anderson Uchôa, 
![Author image](./image2.jpg)

# Ana Carla Bibiano, 
![Author image](./image1.jpg)

# Daniel Oliveira, 

# Alessandro Garcia, 

# Jens Krinke, 

# Emilio Arvonio

# [Conferences]: 
# (MSR 2020 Technical Papers)

>Venu: Mon 29 Jun 2020 10:37 - 10:45 at MSR:Zoom2 - Refactoring & Testing 
>>Chair(s): Mauricio Aniche


# ABSTRACT

Code refactorings are of pivotal significance in contemporary-day code evaluation. Developers can also additionally preserve, revisit, upload or undo refactorings thru adjustments’ revisions. Their intention is to certify that the driving reason of a code alternate is nicely achieved. Developers’ intents
in the back of refactorings can also additionally range from natural structural development to facilitating characteristic additions and computer virus fixes. However, there may be little knowledge of the refactoring practices completed through builders in the course of the code evaluation process. It is likewise uncertain whether or not the builders’ intents impact the selection, composition, and evolution of refactorings in the course of the evaluation of a code alternate. Through mining 1,780 reviewed code adjustments from 6 structures pertaining to 2 large open-supply communities, we document the primary in-intensity empirical observe on software program refactoring in the course of code evaluation. We inspected and labeled the builders’ intents in the back of every code alternate into 7 wonderful categories. By reading records generated in the course of the whole reviewing process, we observe: (i) how refactorings are selected, composed and advanced at some point of every code alternate, and (ii) how builders’ intents are associated with those decisions. For instance, our evaluation suggests builders often observe non-trivial sequences of refactorings that crosscut more than one code elements
(i.E., extensively scattered withinside the program) to help a unmarried characteristic addition. Moreover, we found that new builders’ intents generally emerge in the course of the code evaluation process, influencing how builders pick and compose their refactorings to obtain the new and tailored goals. Finally, we offer an enriched dataset that lets in researchers to analyze the context and motivations in the back of refactoring operations in the course of the code evaluation process.

# 1 INTRODUCTION

Modern code evaluate structures consisting of Gerrit [2, 20] is an increasing number of being followed in each industrial [44] and open-source [43]
projects. Along code evaluations, builders check out and talk the
exceptional of every other’s code adjustments earlier than accepting them. Code
refactoring performs a key function in present day code evaluate [1, 19]. Refactorings are not often left out throughout code evaluate [19]. In addition,
present day code evaluate will increase the attention of builders on
the significance of code refactoring [1, 19]. Refactoring is composed of
making use of one or extra structural code transformations (i.E., refactoring operations) [18] as a way to gain numerous builders’ intents [23, 29, 41] and goals. The intents might also additionally range from natural structural development to facilitating function additions or computer virus
fixes [23, 29, 30, 41].

However, there's little knowledge at the refactoring practices carried out via way of means of builders throughout the code evaluate technique. For
instance, a current examine [46] have determined that Extract Method [18]
operations are typically hired in code adjustments supposed at
facilitating function additions and/or computer virus fixes. However, even for an reputedly easy refactoring type, consisting of an Extract Method, it
won't be clean to get it proper withinside the first attempt [32, 49]. Moreover, builders typically appoint a couple of refactoring operation
to gain a sure goal [6]. As a result, refactoring operations might also additionally be revisited, preserved, delivered or undone in every new revision of a code evaluate. In addition, the builders’ intents might also additionally affect how they choose, compose and evolve refactoring operations throughout the code evaluate technique.

The knowledge of the way refactorings are carried out alongside code
evaluations with various intents is of paramount significance. There is a
developing frame of refactoring strategies withinside the literature [21, 24, 26– 28, 33, 34, 42]. However, it isn't clean whether or not they're properly aligned with the exercise of present day code evaluate. Existing empirical research generally tend to research refactoring operations hired simplest while the developer has the specific purpose of refactoring [6, 40]. Other research clearly examine the frequency of refactorings with unique motivations [46] or intents [23, 41]. Moreover, current literature generally tend
to research refactoring adjustments a posteriori [4, 6, 10, 29, 46], that's a way that offer no context to recognize how builders compose and evolve refactoring operations as a code change evolves. Hence, to the great of our knowledge, there's no examine that plays an in intensity research concerning the relationship among software program refactoring and code evaluate, in particular while thinking about unique builders’ intents and their affect on
refactoring and reviewing practices.

In this paper, we cope with those gaps via way of means of reading how builders
carry out code refactoring withinside the context of present day code evaluate. We have a look at how refactoring differs throughout adjustments pushed via way of means of unique intents. By exploring data to be had alongside every evaluate, we additionally have a look at how builders compose and evolve their refactorings at some stage in every code change. We first accrued code evaluate records of 6 real-international software program structures from massive open source communities. We recognized and analyzed 1,780 code evaluations that hired a complete of 7,259 refactoring operations recognized in 13 typically used refactoring types [29].

To gain our examine goals, we inspected and categorized the builders’ intents at the back of every code evaluate that hired refactoring operations, attaining 7 awesome intents. We in addition recognized and outstanding code adjustments with specific and non-specific refactoring intents. We additionally recognized and analyzed the developments on how builders compose refactorings even as reviewing a code change with specific and non-specific refactoring intents. Finally, we recognized and analyzed 5 refactoring evolution styles determined throughout code evaluate. Our contributions encompass: (i) findings on how refactorings are carried out alongside code evaluations with unique intents, (ii) a dialogue approximately the results of those findings, and (iii) a new enriched code evaluate dataset [39] that lets in researchers to analyze the context and motivations at the back of refactoring operations throughout code evaluate. We summarize our findings as follows:

(1)	As expected, easy refactoring types, consisting of extracting
and renaming methods, are the maximum not unusualplace in adjustments
supposed at including features. However, those easy operations are regularly now no longer implemented in isolation. They are regularly part
of non-trivial sequences of refactoring operations, which: (i) encompass complicated refactorings, consisting of shifting magnificence members, and (ii) are delivered or maybe undone alongside a function-associated change. These observations inspire the research of recommenders that higher aid builders alongside evaluations supposed at including features.

(2)As expected, specific refactoring adjustments regularly contain complicated refactoring operations, consisting of shifting or extracting classes. However, our findings contradict observations made in a current examine [19], which reviews builders do now no longer ignore specific refactoring-associated feedback throughout evaluate. We observed that: (i) those adjustments had lots much less revisions than others, and (ii) the refactoring operations had been not often refined or undone alongside the code evaluate. This is an exciting locating as current research have proven that natural refactoring regularly contributes to new code smells [6, 10] or bugs [3, 17]. These
observations additionally beef up the significance of making use of current strategies for helping builders while performing
specific refactoring [24, 27, 28, 34].

(3) We located that new builders’ intents typically emerge alongside a evaluate and affect how builders choose and compose their refactorings. These observations display how interactive the refactoring technique is alongside code evaluations, i.E., builders generally tend to revisit, refine, and occasionally undo their refactorings primarily based totally on their peers’ feedbacks. This additionally demonstrates the significance of refining current strategies for refactoring conscious code evaluations (e.G., [19]), in order that builders interactively get hold of data and pointers that manual them on refining and choosing refactorings that make a contribution to their intents.
