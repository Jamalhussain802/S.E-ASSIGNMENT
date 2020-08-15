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

# 2 BACKGROUND AND RELATED WORK

# Modern Code Review 

is a lightweight, informal, asynchronous, and usually tool-assisted exercise geared toward detecting and disposing of defects in elements of a software program project [2]. Examples of defects consist of bugs, overall performance issues, (un)intentional violations of design and/or architectural concepts or rules, and fashion violations [5, 50].

The contemporary-day code evaluate method is initiated via way of means of the code proprietor that modifies the unique code base and submits a brand new code alternate to be reviewed. Other builders at the improvement group will serve as reviewers for the code alternate. Each reviewer inspects the code alternate, searching out defects, as defined above. After completing their inspection, every reviewer affords remarks withinside the shape of feedback to the code proprietor. This cycle is repeated till the reviewers attain an settlement to approve or reject the proposed code alternate.

Reviews normally take numerous iterations, along with reviewers
imparting remarks and the code proprietor making next adjustments
in elements of the gadget below evaluate in reaction to the feedbacks
till an settlement is reached. In our study, we use evaluate to suggest
the whole method of a unmarried code evaluate, from filing a brand new
code alternate for evaluate to approving or rejecting the integration
of the alternate into the codebase. In addition, we use revision to
suggest the unique iterations at some point of the cycle of a unmarried evaluate.

# Refactoring and Developers’ Intents. 

Software refactoring is a not unusualplace improvement exercise that goals at enhancing the internal shape of a software program gadget [18]. Previous research have shown that builders practice refactoring now no longer simplest on upkeep obligations however additionally in different obligations of the software program improvement lifecycle [23, 41, 46]. Such research indicated that function including and worm solving are additionally intents builders have once they carry out refactoring. This phenomena has have become recognised withinside the literature as floss refactoring.

The first grasps at the builders’ intents and motivations when
appearing refactoring emerged withinside the research furnished via way of means of MurphyHill et al. [29] and Negara et al. [30], wherein the authors investigated the variations among guide and automatic refactoring.

These research discovered that refactoring operations are usually
carried out along side different varieties of adjustments, typically as
coaching for introducing a brand new function and worm solving.
Silva et al. [46] monitored Github tasks to hit upon refactoring
operations carried out in 124 systems. As those adjustments had been integrated into the systems, the authors carried out electronic mail interviews and surveys with the adjustments authors’ to evaluate their motivations in the back of the refactoring operations. Extracting a technique become cited because the maximum not unusualplace refactoring operation, wherein the main motivation is the coaching for brand new function developments. In preceding work, we carried out an research at the builders’ intents in the back of software program adjustments at some point of code evaluate [36, 37]. 

We robotically diagnosed sizable architectural adjustments and
investigated the context wherein such adjustments had been carried out. 
A comparable research become carried on via way of means of Tufano et al.[54, where in the authors diagnosed the builders’ intents in the back of commits that delivered and eliminated code smells. In a current study, we analyzed refactoring sequences and discovered that builders frequently practice
the identical refactoring kind at some point of a unmarried commit [6]. However, we did now no longer check out how builders compose and practice refactoring sequences primarily based totally on their intents.


# 3 MOTIVATING EXAMPLE

We undertake evaluation 58223 [12] from the couchbase-java-customer system (see Section 4.2) to inspire our empirical take a look at and depict the phenomenon we investigate. Through the path of this unique code evaluation, exclusive factors of the code alternate have been discussed, along with tests, licenses, fashion etc, which caused several changes withinside the supply code. However, to stay concise, we consciousness at the discussions and supply code adjustments related to the developers’ intents and refactoring operations.

Figure 1 offers the refactoring operations finished withinside the lifecycle of evaluation 58223 (see Section 4.2 for info at the refactorings
identity procedure). This evaluation occurred from 01/04/2016
to 01/19/2016, and it's miles composed of 15 revisions, which can be indicated withinside the backside of the figure. The intention for this code alternate was to introduce a brand new set of training to examine precise elements of a JSON document with out the want to technique the entire document, wherein this
inner API can be re-utilized by exclusive elements of the codebase.
An excerpt of the evaluation’s description reads as “[The new] Subdocument API permits to mutate and study precise fragments of JSON
inner an present file while not having to switch the whole
file (...)”. One can sincerely infer from the outline that the
code proprietor had the cause of including a brand new function to the codebase.

Hence, the primary revision is composed in general of recent code being added to put in force the brand new JSON analyzing capability.
In the second one revision, we take a look at the primary refactoring operation accomplished on this evaluation. Before this evaluation started, the elegance JsonTranscoder had a way referred to as jsonObjectToByteBuf() that turned into used to parse a JSON item into bytes to be similarly processed. Since the developer’s purpose turned into to create a widely wide-spread set of software instructions to study JSON files, the unique code from jsonObjectToByteBuf() turned into extracted into a brand new and greater widely wide-spread technique referred to as objectToByteBuf(). Notice that this refactoring operation turned into pushed through the developer’s purpose of including a brand new function, which, on the time this revision turned into submitted, did now no longer completely exist yet. Hence, present refactoring recommenders that awareness totally on structural development [26, 48, 51] might fail to assist the developer on this refactoring activity.

In the next 10 revisions (from r3 to r12), the code proprietor changed elements of the code apart from elegance JsonTranscoder. Thus, the refactoring operation mentioned above remained a part of the code alternate till revision 12. In the meantime, reviewers of this code alternate supplied remarks concerning the codebase shape as a end result of the brand new function being added. One of the reviewers pointed out: “What do you reflect onconsideration on including a DocumentFragment interface and enforcing it as JSON (...) ?”. This remark shows that the builders concerned on this evaluation diagnosed an opportunity
to enhance the system’s shape at the same time as introducing a brand new function.

Hence, from this factor forward, the builders’ cause for this precise evaluation modified from totally including a brand new capability to combining codebase development and function implementation.

As a end result, in revision 13, the code proprietor changed elegance JsonTranscoder again. In this new revision, the writer first reverted the elegance to its unique nation withinside the codebase. Hence, the refactoring operation that has been first accomplished in revision 2 has been undone.
Instead, greater complicated refactorings had been accomplished to mirror the evaluation’s new purpose of enhancing the codebase shape. Method byteBufToClass() has been moved from elegance JsonTranscoder to elegance TranscoderUtils. Next, technique byteBufJsonValueToObject() has been extracted right into a widely wide spread technique byteBufToGenericObject(), which has been later moved to elegance TranscoderUtils. Finally, characteristic LOGGER has been moved from elegance JsonTranscoder to instructions TranscoderUtils and CouchbaseAsyncBucket.

This example depicts extraordinary components of the way the builders’
intents toward a code alternate have an effect on the manner they rent refactoring operations. In addition, it suggests how the iterative nature
of the code evaluation system can also additionally lead builders to alternate their cause all through the path of a evaluation. First, we confirmed how refactoring operations can be hired to assist the addition of recent
capabilities whilst that is the only purpose of a code alternate. Next, the remarks supplied through different builders all through the reviewing system
brought about converting the unique purpose for the code alternate. As a end result, formerly accomplished refactoring operations had been undone and new
refactorings had been accomplished to mirror the brand new intents


# 4 STUDY SETTINGS

# 4.1 Research Questions

# RQ1: What are common refactoring types employed under each specific intent? –

RQ1 goals at investigating the refactoring sorts hired while builders have exceptional intents for a code changebelow review, e.G., function including and malicious program fixing. We degree the maximum and least not unusualplace refactoring sorts hired, their distributions, and the way they range consistent with exceptional intents. By answering RQ1, we're capin a position to show new observations at the refactoring sorts hired below exceptional intents. This is beneficial for researchers while devising refactoring strategies that account for the builders’ intents. Moreover, through studying the builders intents, we depict how refactorings are hired to aid the
author’s unique rationale and intents that emerge at some stage in code review,which has now no longer but been mentioned withinside the literature.

# RQ2: How do developers compose refactoring sequences to support their intents? –

RQ2 pursuits at complementing the knowledge acquired withinside the preceding query with the aid of using investigating how builders compose refactoring sequences, i.E., refactoring operations applied in conjunction, to help their intents. By answering RQ2, we screen new observations approximately how builders compose refactoring sequences to help their intents all through code review. We also spotlight the maximum not unusualplace compositions of refactoring sequences while builders have the express motive of refactoring or not.

# RQ3: How do code changes that employ refactoring operations evolve during code review? –

RQ3 targets at investigating how refactoring operations evolve at some point of the manner of code review. By answering this question, we're capin a position to show 5 exclusive refactoring evolution patterns, supplying new insights at the refactoring practices hired at some point of the reviewing manner. Previous studies [4, 6, 10, 46] simplest investigate refactoring utility a posteriori, wherein one can't have a look at such evolution patterns. By studying refactoring operations even as they're carried out in code review, we are capable of pass ahead the empirical understanding on refactoring practices.

# 4.2 Study Steps and Procedures 

# Step 1: Select software systems that adopt modern code review

We decided on structures supplied through the Code Review Open
Platform (CROP) [35], an open-supply dataset that hyperlinks code evaluate facts with their respective code adjustments. CROP presently offers facts for eleven structures, accounting for a complete of 50,959 code opinions and 144,906 revisions extracted from big open supply communities: Eclipse and Couchbase. All structures in CROP appoint Gerrit [20] as their code evaluate tool. Hence, through the use of CROP, we've get entry to to a wealthy dataset of supply code adjustments that goes past different platforms, consisting of Github. The CROP facts include now no longer handiest the supply code extrade in itself, however additionally all of the feedback and remarks all through evaluate, the extrade’s description evolution, hyperlinks to the problem monitoring gadget and so on. We decided on handiest Java structures protected withinside the CROP dataset because of obstacles of the RefMiner tool [53] (See Step 2). Table 1 offers information about each decided on gadget, wherein the Eclipse and Couchbase structures are provided withinside the top and backside halfs of the table, respectively. We additionally element the wide variety of merged opinions and revisions in each gadget observed through the time-span of our investigation. Finally, we document the median, most and minimal values of kLOC.

# Step 2: Identify refactoring operations during code review

We used the RefMiner device [52] to pick out refactoring operations in keeping with thirteen refactoring sorts which might be usually hired through developers [46]. We have recognized refactoring operations through thinking about every revision of a code change, wherein every revision changed into as compared to its parent, i.E., the codebase’s model earlier than any revision (which include the preceding ones) changed into applied. For info concerning this procedure, we advise a latest empirical study we executed committed to this topic [38]. In research executed through RefMiner’s authors, the device is stated to reap 98% of precision and 93% of recall [46, 52], which makes it the contemporary state-of-the-art device for computerized refactoring detection. RefMiner has been continuously evolved and evolved, wherein the today's strong launch dates from May, 2018. However, its today's model has now no longer been hired in latest research. On the alternative hand, its in advance releases have been used and evaluated in research through researchers apart from the equipment’ authors [10, 17, 29], accomplishing comparable rankings of precision and recall as in its authentic proposed paper. Hence, we selected to appoint an in advance model of RefMiner (model 0.2.0) [52] because of its effects in research executed through each the equipment authors and different researchers.

Table 2 lists the thirteen refactoring sorts recognized through RefMiner. We recognized refactoring sorts that have an effect on special scopes of a code element: 4 sorts that have an effect on a category or interface; six sorts that have an effect on methods; and 3 sorts that have an effect on an attribute. 

We recognized 1,780 code adjustments that hired refactoring operations for a complete of 7,259 refactoring operations executed when thinking about all decided on systems. We additionally located that the share of evaluations that carry out refactoring operations is consistent at some stage in all analyzed systems (from 11% to 14% of evaluations). 

Moreover, maximum of the evaluations have or extra refactoring operations, frequently attaining four or extra. Consider the code overview example mentioned in Section 3, for example. All refactoring operations depicted in Figure 1 had been mechanically identifed through RefMiner. The
entire set of refactoring operations recognized for all revisions in
our dataset is to be had in our replication package [39].

# Step 3: Manually inspect and classify the developers’ intents behind code review discussions.

We taken into consideration all 1,780 critiques that hired refactoring operations to carry out a guide inspection and category of the developers’ intents based at the overview’s description and reviewers’ remarks via comments. 

We finished our guide category through adopting a stateof-the-artwork manner to categorise the developers’ reason in a code alternate [36, 37]. As a part of the manner, we taken into consideration all of the facts worried in a code overview, inclusive of devote messages, discussions among developers, hyperlinks to trouble monitoring systems, and supply code. In this paper, we don't forget the reason of a code alternate to be the dreams and motivations of the alternate’s author(s). Table three lists the developers’ intents we recognized in our study. We offer a description of every reason accompanied through an excerpt from the critiques’ dialogue to function instance of our category procedure.

The guide category procedure consisted of authors studying the facts of every code alternate and figuring out the developers’ reason. We hired a -segment procedure: 1) authors solely and one at a time inspected and labeled all critiques; 2) the authors mentioned all of the code modifications for which there has been a war of words withinside the category. During the category procedure, we recognized critiques with combined intents, i.E, critiques with a couple of reason,inclusive of Feature/Refactoring, and Feature/Refactoring/Bug Fixing. We emphasize there has been no war of words on any code alternate after the 2d level of category. Consider the code overview mentioned in
Section three. Based at the overview’s facts, as defined above, we recognized a Feature/Refactoring reason for this overview. The set of manually labeled code critiques that hired refactoring operations are
to be had in our replication package [39].

# Step 4: Validation of code reviews that present a refactoring intent

Due to RefMiner’s limitations, there is probably code critiques wherein the builders gift a refactoring cause but no refactoring operation is identified. This might bias our look at with the aid of using investigating handiest the code critiques wherein RefMiner is capable of figuring out a refactoring operation, and probably lacking on different critiques with a refactoring cause. To investigate this danger to our look at’s validity, we employ the code critiques’ category finished with the aid of using our preceding work [37]. In this look at, we classified code critiques consistent with their architectural impact. Hence, we can hire this category as a partial floor fact for code critiques that gift a refactoring cause irrespective of the presence
or absence of refactoring operations. Thus, for every assessment formerly reported [37] as having a refactoring cause (332 critiques), we used RefMiner to become aware of the refactoring operations that might had been hired. When thinking about all structures studied in the preceding work, we determined that 196 (59%) of the critiques with a refactoring cause hired at the least one refactoring operation.

Regarding the 136 (41%) ultimate critiques, we finished a qualitative evaluation to analyze the motives RefMiner changed into now no longer capin a position to become aware of refactoring operations.

As a result, we determined that handiest 4% of those critiques contained
fake positives, i.E., critiques that contained refactoring operations
that RefMiner did now no longer become aware of. The records and code for 6% of the critiques changed into noisy and impure, wherein we couldn't qualitatively become aware of whether or not a refactoring operation changed into hired or now no longer. For the opposite 31% of critiques, the builders claimed to be performing a refactoring wherein in truth different adjustments have been finished, such as overall performance improvements, for example. Hence, primarily based totally on these analyses, we investigate that our empirical look at is handiest negligibly tormented by RefMiner’s limitations. Additional information of this validation are to be had in our replication package [39].

