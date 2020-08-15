# How Graduate Computing Students Search When Using an Unfamiliar Programming Language

# Authors:

# Gina Bai, 
![Author image](./image1.jpg)

# Joshua Kayani , 

# Kathryn Stolee
![Author image](./image2.jpg)

# [Conference]: 
# (ICPC 2020 Research)


>Venue: Tue 14 Jul 2020 15:00 - 15:12 at ICPC - Session 7: About Developers 
>>Chair(s): Wahab Hamou-Lhadj

# ABSTRACT

Developers and computing college students are typically predicted to master more than one programming languages. To analyze a brand new language, builders regularly flip to on-line seek to discover facts and code examples. However, insights on how newbies carry out code seek while running with an surprising language are lacking. Understanding how newbies seek and the demanding situations they encounter while the use of an surprising language can inspire destiny gear and strategies to higher assist next language newbies.
Research on code seek conduct commonly includes monitoring builders at some stage in seek sports thru logs or in situ surveys. We carried out a have a look at on how computing college students look for code in an surprising programming language with 18 graduate college students running on VBA obligations in a lab environment. Our surveys explicitly requested approximately seek fulfillment and question reformulation to gather dependable statistics on the ones metrics. By reading the aggregate of seek logs and survey responses, we located that scholars commonly seek to discover APIs or discover instance code. Approximately 50% of queries that precede clicks on documentation or tutorials correctly solved the problem. Students regularly borrowed phrases from languages with which they may be acquainted while attempting to find examples in an surprising language, however time period borrowing did now no longer impede seek fulfillment. Edit distances among reformulated queries and non-reformulated queries have been almost the same. These outcomes have implications for code seek studies, specifically on reformulation, and for studies on helping programmers while gaining knowledge of a brand new language.

# 1 INTRODUCTION

Software is regularly written the use of a couple of programming languages [29,51], which expects the builders to grasp a couple of programming languages. Recent studies has proven that understanding of 1 language can intervene with studying a brand new language [41, 43]. Whenstudying a brand new language, builders use an opportunistic studying strategy, bearing on principles in a brand new language to their preceding languages [43]. As the terminology among languages regularly differs drastically, this makes code seek specially difficult.

Yet, builders often turning to code seek to locate code examples to examine from [39] and enhance their productiveness throughoutimprovement activities [5, 39, 53]. Studies on code seek in software engineering [7, 8, 34, 45, 46, 48] are seeking for to apprehend how and why builders seek while acting their every day paintings [21, 27, 39, 54],introduce new code seek gear or endorse capability improvementof current code seek gear [3, 7, 28, 56], and advocate effective code seek strategies [11, 18]. The code seek research are most regularly completed with inside the wild, as a way to take a look at builders throughout their ordinary activity.

As previous paintings has discovered problems while builders seekfor principles in a brand new language [43], we've got cause to believe that code look for next language freshmen is exclusive thancode seek throughout ordinary improvement activities. Consider the following scenario:
In this scenario, the intern cannot locate the assets they want because of mismatched terminology among the language they know, Java, and the language they need, VBA. This not unusual place scenario is discovered in previous studies [42]; on this exploratory paintings on code seek, we goal college students studying a brand new language.

Understanding and addressing the demanding situations freshmen encounterthroughout seek should cause higher seek reports for freshmen,specially college students, who've much less revel in than the professional builders with studying a next language. Therefore, we layout a look at that entails responsibilities in a language surprising to the contributors and recruit graduate college students in Computer Science as contributors.

Our technique entails logging seek and browser activities and periodically surveying contributors approximately their cutting-edge responsibilities,much like previous paintings [39]. However, in contrast to previous paintings, we particularly discover the elements that cause seek achievement (RQ3), which is decided with the aid of using explicitly asking contributors if a seek become a hit. Prior human research with code seek do now no longer suggest what elements cause a hit searches, in massive element due to the fact obtaining proof of seek achievement is tricky. Relying on end result clicks [14] is incomplete as regularly the solution seems with inside the preview accompanying a seek end result. Relying on proof of question reformulation can reliably locate failed searches [20, 24], however now no longer a hit ones. We deal with this shortcoming the use of in situ surveys that particularly ask approximately seek achievement.

Given the similarity in technique, wherein appropriate, parallels are drawn among the freshmen in our look at and professional builders from a comparable look at at Google [39]. While the contexts of the research numerous widely (i.e., ordinary developer workflow [39]with Google Developers vs. a lab look at with college students running with an surprising language), similarities and variations shed mild on how we can be capable of teach next language freshmen to use seek higher of their workflow, or construct a higher seek device to facilitate greater a hit searches. We summarize our contributions as follows:

• insights at the elements that make a question a hit,

• higher know-how of the code seek behaviors of next language freshmen, and the similarities and variations of seek behaviors among freshmen and professionals, and

• pointers on enhancing the achievement of searches while freshmen are running with an surprising language.
To our understanding, we're the primary to look at how next language freshmen [6, 19, 32, 41] carry out code seek, and our result shave implications for a way to higher guide them. Our principal findings and pointers consist of:

• Successful searches use herbal language phrases, such as “if statement,” in preference to coding shortcuts, such as “if”.

• Successful searches greater regularly seek advice from legitimate documentation and tutorials with instance code in preference to Q&A sites.

• Reformulations arise plenty greater fast after a preceding question than trying to find a brand new topic. The Levenshtein distance among successive queries by myself might not suggest are formulation

• As time period borrowing become generally discovered in seek queries, an “API translator” that could map APIs throughout languages could help next programming language freshmen.

• Since freshmen regularly seek to discover language syntax, APIs/libraries, and instance code, we inspire CS educators to consist of quick pattern code while imparting or requiring use of recent APIs/libraries.

This paper describes the context and strategies we used to collect the surveys and logs for this look at in Section 2. Section three provides the distinct look at results. Implications of the findings are suggest edin Section 4.2 and the capability threats to validity are mentioned in phase 4.4. Finally, Section 6 provides a few concluding remarks and indicates adjustments on destiny paintings

# 2 STUDY

We frame this study around the following three research questions: 
      
    RQ1: Why do subsequent language learners search? 
    
    RQ2: What does a typical search session entail for a subsequent language learner?
 
    RQ3: What are the factors that impact the success of search queries for subsequent language learners?

# 2.1 Study Design

Using a aggregate of surveys and logs, Sadowski, et al. [39] explored the quest conduct of Google developers; it's far from this look at that we derive our methodology. Table 1 summarizes the similarities and variations of the context and accumulated information between the preceding look at and this look at. To goal next language learners, we run our look at in a lab surroundings with graduate students. Participants had been given duties withinside the strange languages. Due to the experimental context, we had been capable of acquire more survey responses in line with question compared to the preceding look at, supplying a better density of auxiliary statistics in line with question.

One of the shortcomings of the authentic look at is that there became no perception of seek achievement with inside the logs or the queries. That is, It became now no longer clean from the information whilst a seek consultation became successful or unsuccessful. To deal with that shortcoming, on this look at, we ask explicitly approximately seek achievement in surveys, one deployed whilst a tab is closed (Figure 4) and any other deployed whilst it's far suspected aquestion is reformulated (Figure 3). Another shortcoming is the use of edit distance to locate reformulation, which might not constitute real reformulation; we deal with this via way of means of asking contributors whethertheir contemporary question is meant to remedy the equal trouble as the preceding question in a reformulation survey (Figure 3).

# 2.2 VBA Programming Tasks

We selected Visual Basic for Applications (VBA) due to the fact it's far a popular programming language with many on-line resources [4, 13], however it's far now no longer usually utilized by the graduate college students in Computer Science at North Carolina State University (NCSU, our player population.Each venture consists of a preferred gaining knowledge of intention (e.g., conditions and loops, string manipulation), a venture description with requirements, and a pattern output/end result for the venture. The 5 tasks 1aresummarized as follows: 

Task 1 gives members a listing of numbers in a column, and asks members to document a macro and create a button that returns the common cost of the numbers on this column whilst the button is clicked. This venture may be finished with or with  out VBA code.

Task 2 calls for members to create a button that creates a message container with "Hello World!" on it as soon as clicked.

Task 3 gives members a listing of ratings in a column referred to as Grade, starting from forty three to 100, and ask members to create a button that populates a column referred to as P/F with P or F for Pass or Fail, respectively, relying on Grade: P is for a score this is more than or same to 60 in column Grade, and otherwise.

Task 4 gives members an unsorted stock listing of unique labels in a column referred to as Item with their fees indexed in a column referred to as Price. Their intention is, given a separate goal listing of labels, to create a button that populates a column Price for the objects with inside the goal listing primarily based totally at the stock listing. The Excel integrated characteristic VLOOKUP isn't always allowed on this venture.

Task 5 gives members a listing of telecell smartphone numbers with inside the layout of (XXX)XXX-XXXX, and asks members to create a button that populates a column referred to as Area Code with unique location codes and their related counts in a column referred to as Count.

# 2.3 Data Collection

We evolved a Google Chrome extension2that information searchactivities and surfing records and deploys surveys. To seize the questions the members are looking to solve, we spark off customers with brief surveys periodically. In this way, we're capable of integrate the survey responses with logs analysis.

# 2.3.1 Tool Implementation. 

The implementation includes parts: a consumer-aspect Google Chrome browser extension for logging facts and a Flask net server for storing facts. On the consumer aspect, the browser extension does the following: 1) initialize browser nearby garage that holds the log statistics, inclusive of issuing aprecise 10-digit ID quantity to every participant, 2) song Google searches, three) song hyperlink clicks on all pages, 4) discover viable questionreformulations thru word-stage Levenshtein distance (if distance ≥  words [23]), 5) layout and installation the surveys, and 6) ship all accumulated logs to our server for garage. All accumulated facts are stored in a password-secured SQLite database on an encrypted server.

# 2.3.2 Procedure. 

The  examine become performed in a lab putting over sessions, 90mins every. Participants attended one lab sessiononly. Participants had been informed to put in the Google Chrome extension on their private laptops and preserve the extension enabled at some stage in the lab session.

# 2.3.3 Surveys. 

To keep away from over-taxing the members, a maximum of 10 surveys in keeping with hour had been deployed with a one-minute minimal c programming language among surveys. A survey is induced while a participant plays one of the following 4 actions:

(1) Finishes installing the extension
Preliminary Survey (Figure 1). We gather members’ technical historical past together with programming experience, their intentions of code search, and demographic statistics.

(2) Makes a search
Context Survey (Figure 2). We ask members approximately the sports they're doing, and the particular query they' resolving. Questions Q2, Q3, and Q5 are from earlier work [39].In addition, we ask what approach(es) they’ve followed to clear up the tasks.

(3) Reformulates a query
Query Reformulation Survey (Figure 3). A question is identified as a ability reformulation if its word-stage Levenshtein distance from the earlier question is more than or identical to. This survey verifies the reformulation with the aid of using asking in the present day question is associated with the preceding one. It additionally asks if the earlier question solved the problem. If so, how did it help; if now no longer, what statistics is missing.

(4) Closes the tab Search 
Tab Closed Survey (Figure 4). This survey asks if the earlier question solved the problem. If so, how did it help; if now no longer, what statistics is missing.
A survey will now no longer be induced with the aid of using any occasion if the earlier survey is deployed inside a minute or the quantity of deployed surveys has reached the hourly limit.

We requested members to finish the survey whenever it is deployed, despite the fact that of of entirety isn't always forced.

# 2.3.4 Log Data. 

A log access is created while a player performs one of the following cause events: searches, closes a tab, clicks a link, switches tabs, or switches to every other application. The logged facts includes:

• UserID: A specific wide variety that distinguishes participants.

• Time: Time of this activity.

• Type: Types of browser activities, including: closed the tab, clicked a link, deployed survey, acquired survey responses.

• URL: The url of the internet site the player clicked.

• TabID: Browser-assigned ID for every tab to tune the tab activities.

• Query: String from a web seek query


# 2.4 Participants

We invited college students enrolled in a graduate software program engineering direction at North Carolina State University thru e mail to participate with inside the study (reaction rate: 42.6%). A quick advent to this study, inclusive of the reason thereof, and the tool (Google Chrome extension) used with inside the study, became made to be had to all potential individuals. As compensation, individuals who've the extension enabled and recording for at the least 45mins have been eligible to go into right into a drawing to win a $30 Amazon present card. In overall 23college students finished the preliminary surveys. After discarding statistics from5 individuals whose interactions have been recorded for much less than 10mins, we have been left with statistics from the closing 18 individuals for analysis (average: 78.5mins, median: 84mins, which consists of 4 girl college students and fourteen male college students.

The 18 individuals self-said their knowledge in fashionable programming skills: one as a beginner developer, 5 as experts, and twelve as intermediates. Two individuals claimed to have prior operating enjoy with inside the industry. All individuals regularly seek on web sites for code, and the bulk of individuals every now and then or regularly ask buddies for help (16/18) or seek on IDEs (16/18). Participants got here from a various programming language background, inclusive of object-orientated programming languages and scripting languages, however now no longer VBA. The pinnacle 5 common programming languages utilized by the individuals have been: Java, JavaScript, C++, C, and Python.

# 2.5 Analysis

We grouped the logs via way of means of contributors’ IDs and looked after them via way of means of log time. Surveys had been tabulated and related to browser events for evaluation. Logs had been analyzed to acquire 1) seek queries, 2) ordered listing of clicked internet site URLs related to every question, and3) time spent via way of means of a player on a clicked end result page.

The logs had been break up into seek sessions. Due to our take a look at context, adopting the definition of a seek consultation from the take a look at on Google developers [39] became problematic. When thinking about a seek consultation as a chain of developer sports separated via way of means of 6-mins of inactivity, every player in our take a look at had precisely one seek consultation. Thus, we deal with every seek question and its associating end result clicks as one seek consultation (mentioned as “micro-consultation” in earlier paintings [39]).

Our reformulation surveys had been deployed while the Levenshtein distance became or greater, consistent with earlier paintings [23, 34]. If contributors solution sure to Q1 (Figure 3), this suggests that the modern-day question isn't a reformulation and starts a brand new subject matter. If the player solutions no to Q1 and sure to Q2_n, which means the preceding question did now no longer remedy the query and the modern-day question is associated with the equal trouble, and hence the modern-day question is are formulation. If a player solutions no to Q1 and no to Q2_n,we anticipate that the trouble is the equal however the player is attempting a brand new approach, and hence the question isn't a reformulation. While earlier paintings makes assumptions approximately reformulation base don subject matter evaluation or question distances, those survey responses serve as a floor reality for reformulation evaluation. While we do now no longer have sufficient facts to construct a classifier to are expecting reformulation, we can examine the context round regarded reformulations as opposed to regarded non-reformulations.

