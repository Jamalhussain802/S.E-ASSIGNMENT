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


#  5 RESULTS AND DISCUSSION 

# 5.1 Refactoring Types per Review’s Intent

# Refactoring operations and intents. 
We deal with RQ1 through studying the distribution of the wide variety of opinions that hired refactoring operations grouped through builders’ rationale and refactoring kinds. Next, we examine the maximum and least not unusualplace refactoring kinds hired, consisting of their distributions, and the way they vary in step with specific intents. Figure 2 illustrates the distribution
of code opinions that hired refactoring operations grouped through
the developer’s rationale.

# Figure 2: Distribution of reviews that employed refactoring operations grouped by developer‘s intents and systems

The parent suggests that maximum of the code adjustments that appoint
refactoring operations gift a Feature rationale, accounting for 54.5%
of all opinions. In 27.3% of the opinions, builders have the sole
rationale of Refactoring. Bug Fixing seems because the 1/3 maximum not unusualplace rationale: builders refactored the device to restoration a malicious program in 11.9% of the opinions. Finally, the wide variety of opinions recognized with the rationale of Feature Removal, Platform Update and Merge Commit are negligible in evaluation to the maximum famous intents previously discussed. These consequences suggest that builders maximum commonly
appoint refactoring operations after they do now no longer have an express rationale of refactoring, i.E., the refactoring is blended with different adjustments, usually for enforcing a brand new characteristic or solving a malicious program. These observations partially supplement preceding research concerning builders’ intents and motivations in the back of refactoring [23, 41, 46], strengthening the empirical proof on this topic.

# Refactoring types and non-explicit refactoring intents.

Table 4 provides the wide variety of opinions that hired refactoring operations grouped via way of means of the builders’ reason and refactoring kinds. Each mobileular represents the wide variety of opinions that hire a sure refactoring kind whilst having a sure reason. In Table four, we do now no longer take into account the wide variety of refactoring operations of the identical kind used withinside the identical assessment. Instead, we without a doubt take a look at if a assessment employs a sure refactoring kind or now no longer. 

Differently from preceding studies (e.G., [29, 40, 46]), our method allows us to become aware of intents that emerge at some stage in code assessment to assist the belief of the unique reason. We talk over with those intents as blended intents, i.E., opinions that had as a minimum distinct intents, which includes Feature/Refactoring, Refactoring/Bug Fixing, and Feature/Refactoring/Bug Fixing. Hence, for the the rest of this study, we speak unmarried and blended intents separately. To keep away from misunderstandings, we talk over with the unmarried intents as Feature Only, Refactoring Only and Bug Fixing Only. Finally, we differentiate intents with an specific reason of refactoring from their non-specific counterparts, in which the primary are offered in a grey history and the latter are offered in a white history in Table 4. 

Table 4 suggests that a substantial wide variety of refactoring operations are focused in opinions with the intents of Feature Only, Feature/Refactoring, Refactoring Only, and Bug Fixing Only. 

Table 4 lets in us to look at that for non specific refactoring opinions, i.E, Feature Only, Bug Fixing Only, and Feature/Bug Fixing, as much as 48% and 26% of opinions hired Extract Method and Rename Method, respectively. Other refactoring kinds are much less common than approach extraction and renaming. Each of the alternative refactoring kinds happens in much less than 10% of the non-specific refactoring opinions. 

In summary, we located that extracting and renaming techniques are the maximum common refactoring operations no matter the reason. This end result gives a distinct attitude at the observations made via way of means of a preceding study. Silva et al. [46] indexed eleven motives that encourage builders to use Extract Method. Most of those motivations challenge the development of the system’s inner structure. However, we located in our motivating example (see Section 3) that the motivations for extracting a way can cross past the indexed ones. In our example, the builders implemented an Extract Method refactoring to assist the implementation of a brand new feature. 

# Refactoring types and explicit refactoring reviews.

For the critiques with an specific rationale of refactoring, i.E., Feature/Refactoring and Refactoring Only, a much broader variety of refactoring types are hired while in comparison to their non-specific counterparts. For such critiques, Extract Method continues to be the maximum not unusualplace operation with 21% of critiques, even as Rename and Move technique are the 2d and 0.33 maximum not unusualplace operations with 16% of critiques.
For critiques with the Feature/Refactoring rationale, builders move
training throughout programs in handiest 5% of the critiques. Classes are greater regularly moved (12%) in critiques with a Refactoring Only rationale.

A comparable statement applies for the Rename Class refactoring, that's greater hired in critiques with Refactoring Only
rationale than Feature/Refactoring. Moreover, refactoring operations
regarding training take place greater frequently in Refactoring Only (25%) and Feature/Refactoring (21%) critiques. As for non-specific refactoring
intents, class-stage refactoring operations variety from 7% (Bug Fixing
Only) to 13% (Feature Only).

# 5.2 Refactoring Sequences per Review’s Intent

In RQ1, we determined that builders did now no longer follow remoted refactoring operations of various types. Thus, we hypothesize that refactoring operations is probably implemented in compositions. Hence, we completed an evaluation to acquire an in-intensity information on how refactoring sequences are composed below exceptional intents.

Identification of Refactoring Seqences: We accrued refactoring sequences that have been implemented for the duration of the assessment manner of a code change. We taken into consideration that a refactoring series consists of or extra interrelated refactoring operations implemented in next revisions of a code assessment. Two refactoring operations are interrelated whilst they may be implemented in a not unusualplace set of code factors (e.G. Classes). This method has been implemented in latest empirical research concerning refactoring sequences and compositions [6, 7, 47]. We analyzed the refactoring sequences for the following intents: Feature Only, Refactoring Only, Feature/Refactoring and Bug Fixing Only. We consciousness our analyses on those intents
due to the fact they may be the maximum generally determined in our dataset (see Section five.1). Consider assessment 58223, as depicted in Section 3. The refactoring series recognized for this assessment consists of 6 refactoring operations, namely: [Extract Method, Move Method, Extract Method, Move Method, Move Attribute, Move Attribute].

Table 5 affords the variety of refactoring sequences, the variety of refactoring operations that compose the sequences, the variety of opinions, and the variety of revisions for every purpose. When thinking about the 336 opinions and 3,027 revisions that gift a Feature Only purpose, we recognized 426 refactoring sequences composed of a complete of 1,621 refactoring operations.

Our consequences imply that 3,437 (47.34%) out of 7,259 refactoring operations have been implemented in sequences, in which those sequences are disbursed in an average of five revisions. Besides that, builders implemented refactoring sequences on 580 (25.14%) out of 2,307 opinions. Moreover, word that a few opinions had multiple refactoring series, together with the Refactoring
Only purpose. In this precise case, we observed that builders implemented refactoring operations in exceptional units of code factors for the duration of
those opinions, which symbolize exceptional refactoring sequences.
In addition, we've got determined a complete of 250 (33.55%) out of 745
refactoring sequences in opinions in which builders had the explicit
purpose of refactoring (Refactoring Only and Feature/Refactoring.

# Table 5: Number of refactoring sequences per intent

Aimed at know-how how those refactoring sequences are
composed, we created 4 classes primarily based totally at the code element’ scope of every refactoring kind. Table 6 provides every class accompanied with the aid of using an outline and the refactoring kinds that compose the class. In addition, we gift the predominance of every class over the others while refactorings of various classes are hired in sequence. Finally, we element the wide variety of classes every class of refactoring kind affects. All those attributes will be used on this segment to offer insights on how builders compose refactoring kinds to gain their intents.

# Table 6: Categories of refactoring types

Combination: The class via way of means of aggregate became primarily based totally on findings of preceding research, which investigated how refactoring sorts are blended in refactoring sequences [6–8, 47]. However, those research do now no longer look at how those combos relate to builders’ intents. We categorized the refactoring sequences in line with the kinds in their refactoring operations and the order in their combos. Consider the refactoring collection for the instance mentioned in Section 3: [Extract Method, Move Method, Extract Method, Move Method, Move Attribute, Move Attribute]. This refactoring collection is classed into: magnificence, Motion,
Intra-magnificence, Motion, Motion, Motion}. 

As a end result of this class, we've discovered 41 combos of those classes in our data. When thinking about critiques with a Refactoring Only rationale, out of the a hundred and fifty refactoring sequences, 32 (21.3%) are composed of Motion handiest refactoring operations; 29 (19.3%) are composed of Motion and Intra-magnificence refactorings. These effects imply that builders have implemented a non-negligible number (40.6%) of refactoring sequences that have an effect on multiple magnificence, and that they had composed non-trivial refactoring sequences with specific refactoring sorts while having an express rationale of refactoring. Differently, while thinking about the alternative intents, we observed 212 (49.7%) and 38 (55%) Intra-magnificence handiest refactoring sequences for the Feature Only and Bug Fixing Only, respectively. These effects recommend that builders extra regularly implemented refactoring sequences on unmarried code factors while the rationale became now no longer to explicitly refactor the code.

We have discovered one hundred refactoring sequences in critiques with a
combined Feature/Refactoring rationale. Out of those, 26 are composed of
Motion-handiest refactoring operations, and eleven are composed of refactoring operations. This suggests that builders regularly (36%) implemented refactoring sequences on multiple magnificence after they had multiple rationale. Developers regularly implemented a selected order of those classes, via way of means of first shifting instructions, subsequent enhancing instructions hierarchy, and subsequently shifting instructions to guide those intents. This shows that the order in which refactorings are hired is laid low with the specific intents builders have toward the code change. We offer the complete classes’ class in our replication package [39].

# Refactoring sequences with Extract Methods or Rename Methods.

On combos which have the kinds Intra-elegance or Rename, we found that 518 (69.53%) have as a minimum one Extract Method, and 94 (12.61%) have as a minimum one Rename Method. Previous paintings mentioned that Extract Method and Rename Method are the maximum not unusualplace refactoring kinds implemented while assessed in isolation [10, 46.However, our outcomes gift that those refactoring kinds are frequently implemented along side different refactoring kinds. Predominance: We described the predominance class based at the scope that every class affects. Categories that have an effect on a massive scope predominate over classes that have an effect on a small scope.

Thus, the order of predominance, from the most important to the smallest
scope, is as follows: Hierarchical, Motion, Intra-elegance, and Rename.
As formerly shown, the assessment mentioned in Section three provides
a refactoring collection of [Extract Method, Move Method, Extract
Method, Move Method, Move Attribute, Move Attribute], which yields a classes’ class of {Intra-elegance, Motion, Intra-elegance, Motion, Motion, Motion}. According to Table 6, the Motion class has predominance over Intra-elegance regardless the refactorings order. Thus, this refactoring collection can be categorised surely as Motion. Table 7 provides the predominance of classes for every rationale. Consider the Feature Only rationale, for example. We take a look at that 212 refactoring sequences are categorised into predominantly Intra-elegance, which bills for 49.77% of all refactoring sequences with a Feature Only rationale. Developers frequently implemented classes that involved a massive code scope after they had the specific rationale of refactoring.We have determined that 93 (62%) out one hundred fifty refactoring sequences with Refactoring Only rationale hired code movement among classes. In addition, 10 (15%) out those hired refactoring operations on hierarchical classes, wherein those refactoring sequences have a mean of 12 refactoring operations. This suggests that builders frequently implemented refactoring on multiple elegance in sequences wherein the rationale is to explicitly enhance the structural quality.

# Refactoring sequences and Feature Only intent.

When thinking about the 426 refactoring sequences in critiques with a Feature Only intent, we've got determined that builders hired Motion
and Hierarchical refactoring operations in 140 (32.86%) and 30
(7.04%) of them, respectively.
 	
# Refactoring sequences and Bug Fixing Only intent.

In 25 (36.23%) out of sixty nine refactoring sequences in critiques with a Bug Fixing Only intent, builders hired code movement refactoring operations. This is a stunning observation, as one could expect that transferring code factors among training isn't a not unusualplace exercise to restore insects. Previous paintings have investigated the relationship among refactoring and malicious program fixing [4, 17]. However, those research have investigated remoted refactorings rather than sequences. Hence, our examine is the primary to look at that combos of Move Attribute, Move Method and Move Class refactorings are used for malicious program fixing. For instance, in overview 99067 [15] from jgit, builders implemented a refactoring collection composed of [Extract Method, Move Method, Move attribute] regarding training OpenSshConfig, OpenSshConfig.Host, and OpenSshConfig.State. This refactoring collection become implemented to restore an present malicious program as cautioned during overview: “This avoids some insects in Jsch’s OpenSSHConfig (...)”.

Number of Classes: This category is primarily based totally at the number
of training that every class can have an effect on in refactoring sequences.
The classes that have an effect on a big scope frequently have an effect on greater training than classes that have an effect on a small scope. Thus, the Hierarchical and Motion classes are taken into consideration classes that have an effect on multiple training, and the Intra-magnificence and Rename are classes that have an effect on a unmarried magnificence (see Table 6). This category takes into account the order of the utility of every class. Hence, keep in mind the  instance mentioned in Section 3. A refactoring collection composed of [Extract Method, Move Method, Extract Method, Move Method,
Move Attribute, Move Attribute], could yield a category of.
	 
# Non-trivial refactoring sequences and explicit refactoring reviews	

Table eight gives the category of refactoring sequences concerning range of instructions. One may also word that 60% of the refactoring sequences with a Feature Only motive were labeled as. We located that each time builders have the express motive of refactoring, the sequences normally begin on a couple of instructions (54% and 57% for Refactoring Only and Feature/Refactoring, respectively). In contrast, whilst builders produce other intents, most sequences impact only unmarried instructions (60% and 59% for Feature Only and Bug Fixing Only, respectively). This range of sequences that have an effect on a couple of instructions in critiques with express refactoring intents leads us to agree with that the unmarried magnificence refactorings hired in those critiques, consisting of Extract Method and Rename Method, are frequently used to aid the refactorings that have an effect on a couple of instructions.

# Interactivity, non-explicit intent and mixed-intent

Curiously, builders wanted greater revisions (a mean of 6) while they
commenced with classes that worried a couple of classes (Hierarchical
and Motion) in refactoring sequences to guide the Feature Only
rationale. On the opposite hand, builders additionally wanted greater revisions (a median of 5) in sequences that guide the Bug Fixing Only rationale. Besides that, the refactoring sequences with the Feature/Refactoring
rationale are composed of a mean of seven revisions. Thus, the reviews
which hired refactoring sequences to guide a non-explicit rationale of refactoring and/or multiple rationale require greater interactivity amongst reviewers. This interactivity lets in for discussions on a way to compose refactoring sequences to wait different intents, as provided in our motivating example (see Section 3).

# 5.3 Refactoring Evolution Across Reviews

We cope with RQ3 via way of means of providing a brand new class to represent refactoring evolution styles at some stage in code assessment. We are the primary to look into this phenomenon; hence, we observed a coarse-grained approach whilst reporting those observations as a first-time visualization of this data. Thus, our class serves as a baseline for destiny studies. This class includes acting a sequential commentary of the refactoring operations hired throughout all revisions withinside the code assessment. Consider a code assessment with three revisions, for instance. We sequentially in comparison the refactoring operations achieved withinside the 2nd revision to the refactoring operations achieved withinside the first revision. Next, we in comparison the refactoring operations withinside the 0.33 revision to those withinside the 2nd revision. This method enabled us to have a look at 5 possible refactoring evolution styles.

We describe every sample as follows: 

(i) single, whilst a assessment
has most effective a unmarried revision and at the least one refactoring operation; 

(ii) new, whilst at the least one refactoring became created in a next revision and this refactoring has now no longer been undone in destiny revisions of the equal assessment; 

(iii) undone, whilst at the least one refactoring eration became undone in a next revision of the equal assessment, and no new operations have been identified; 

(iv) both, whilst each new and undone refactoring operations are identified, no matter the order; and 

(v) same, whilst precisely the equal set of refactoring operations
is found in all revisions of a assessment. These styles are mutually
different and incorporate all code modifications in our dataset. Consider
our motivating instance depicted in Section 3. No refactoring operations have been hired withinside the first revision. In the second one revision, an Extract Method refactoring became achieved, which characterizes a new refactoring operation on this assessment’s lifecycle. However, in revision 13, this Extracted Method became undone, and different refactoring operations have been hired instead. Hence, this assessment is considered to have a both refactoring evolution sample.

# Intents and refactoring evolution patterns.

Figure 3 shows the distribution of evaluations grouped with the aid of using the intents and refactoring evolution styles. We discovered that the evolution of refactoring operations in evaluations with the Feature Only and Feature/Refactoring intents have  a tendency to observe extra complicated evolution styles than evaluations with the express rationale of Refactoring Only. While almost 50% of evaluations with the Feature/Refactoring rationale have refactoring operations added, undone or each alongside the revisions, most effective around 25% of the evaluations with the Feature Only rationale have refactoring operations added, undone or each alongside the revisions. Differently, evaluations with the express rationale of Refactoring Only have a tendency to in large part continue to be the identical at some stage in reviewing, with most effective 23% of the evaluations supplying any extrade withinside the refactoring operations. 

These outcomes imply that evaluations with a refactoring rationale
have a tendency to observe a ‘one and done’ behavior, in which maximum of them are incorporated as quickly as they may be proposed. On the opposite hand, featurerelated evaluations have a tendency to be iterative, in which diversifications of the code extrade are normally discovered. We additionally discovered that evaluations with a Bug Fixing Only rationale have a tendency to act further to featurerelated ones. However, evaluations with a unmarried revision seem to be extra common on Bug Fixing Only evaluations in evaluation to Feature Only and Feature Refactoring evaluations.


# 6 STUDY IMPLICATIONS

Our findings offer 3 key implications to be in addition discussed
and that ends in implications for each researchers and device builders.

# Understanding the influence of intents on refactorings.

Many current strategies for recommending refactorings are designed to help builders in acting natural structural development with at the least 3 goals: (i) natural refactoring of a particular module or the complete program [28], (ii) casting off code smells [11, 21, 26, 27, 33, 34], or (iii) re-architecting a system [14, 24, 31, 42]. However, our examine discovered that refactorings are much less commonly carried out in adjustments with the only reason of both optimizing or enhancing the low-degree shape of a class (or one or greater methods), its structure or maybe a particular module. Developers most regularly rent refactorings collectively with different adjustments to help different intents, along with function additions and trojan horse fixes (Section 5.1). Moreover, our findings additionally display that the change’s purpose exerts an have an effect on on: (i) the kinds and scopes of a refactoring (Section 5.1), (ii) the composition (Section 5.2), and (iii) the evolution (Section 5.3) of refactoring operations alongside a change. Previous research did not look into the function of intents on how refactorings are performed, composed and advanced at some point of the code evaluate process.

# There is little support for refactoring with specific intents.

Our aforementioned findings advise there's room for featuring recommenders that higher aid builders in performing refactoring while the code alternate entails multiple intent. For instance, refactoring recommenders that particularly aid characteristic additions or worm fixes have to prioritize refactorings that enhance the shape of the strategies or training which might be possibly to be impacted with the aid of using the brand new capabilities and/or worm fixes. However, existing multi-goal refactoring methods are frequently described in terms of goal capabilities that seize code or layout shape metrics [28, 34], which aren't healthy for maximum of the eventualities we observed in our take a look at concerning distinct intents. Developers may additionally want right steering in those instances as the refactoring evolution styles of such adjustments have a tendency to be more complicated than the ones observed in Refactoring Only adjustments (Section 53). 

Recent improvements on characteristic mining [25, 45], alternate impact
analysis [22] and worm location [13] will be explored to streamline refactorings’ recommendations (and their prioritizations) which might be much more likely to be applicable to floss refactoring duties at hand. For instance, those strategies may be used to: (i) examine the textual description of an upcoming characteristic and worm restore troubles and/or ongoing
discussions alongside a review, and (ii) decide application locations which might be possibly to be suffering from upcoming adjustments.

# Enabling automatic support to refactoring along change’s revisions.

Our findings endorse that builders want extra interactive assist for revisiting, refining and occasionally undoing refactoring choices at some point of the change’s review. First, new intents oftenemerge alongside adjustments (Section 5.1) that appoint refactorings. Second, many refactoring sequences have extra than 3 revisions(Section 5.2). These observations display that the decision-makingmethod on composing refactorings is certainly now no longer a cut-and-driedtask. Reviewers undergo cycles to agree or disagree on a certainrefactoring sequence. They may want to have a look at the effect of a efactoring counseled in a revision first to be able to make the following refactoring choices earlier than in the end approving the change. Qualitative research that specify the influential elements governing thismethod want to be carried out withinside the future. Hence, device builderswant to help builders in knowledge how the code shape development finished with refactorings is facilitating otheradjustments, which includes characteristic additions. Thus, a device to assist refactoring alongside adjustments ought to also: (i) pick out the developer’s intentvia code adjustments and reviewers’ remarks interactively [16],(ii) spotlight how refactorings in a change [19] are associated with suchintents, and (iii) propose the following refactorings to assist thesoftware in their intent.


# 7 THREATS TO THE VALIDITY

# Construct and Internal Validity.

The kind of refactoring sortsanalyzed in our look at may not be representative. To mitigate thisrisk, we decided on refactoring sorts which have been extensively investigated through preceding studies [4, 6, 10, 29, 30, 46]. Another constructrisk issues the order of the refactoring operations that compose a refactoring collection. To alleviate this, our heuristic forrefactoring collection identity take into account the order of every revision to make sure the refactorings are interrelated. Moreover, wequalitatively verified every refactoring collection to assure thatall refactoring operations have been implemented on a not unusualplace set of code elements. We hired RefMiner [52] to locate refactoring operationsexecuted all through code review, whose accuracy has been reportedto be high [9, 10]. In total, we detected thirteen refactoring sorts evenaleven though a few refactoring catalogs record extra than 70 refactoringsorts. Thus, it's miles feasible that a number of the critiques we taken into considerationnow no longer to carry out any refactoring virtually hired operations thataren't supported through RefMiner. To mitigate this risk, we manuallyverified whether or not for critiques while the developer has an explicitmotive of refactoring they hire any refactoring operation basedon a partial floor truth [36]. As a result, we taken into consideration RefMinerperfect for our empirical investigation.

# Conclusion and External Validity.

Regarding the quantitative records evaluation, we tabulated and established all extracted recordsin pairs. The evaluation observed famous hints of descriptive records evaluation [55]. Regarding the qualitative evaluation of thedevelopers’ intents, we hired a  section guide classification technique primarily based totally on cutting-edge empirical studies. In the first section, all code adjustments had been labeled with the aid of using authors. In the secondsection, for all code adjustments in disagreement, each authors discussedto attain a unified classification. Our examine specializes in investigatingthe refactoring sports of Java tasks only. Nevertheless, wespotlight that Java is one of the maximum famous programming languages in each enterprise and academia. Additionally, we investigatedsix real-global structures from big open supply communities

