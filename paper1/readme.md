# Detecting Video Game-Specific Bad Smells in Unity Projects

# Authors
## 1 Antonio Borrelli 

## 2 Vittoria Nardone

## 3 Giuseppe Di Lucca 

## 4 Gerardo Canfora 
![Author image](./image1.jpg)

## 5 Massimiliano Di Penta
![Author image](./image2.jpg)

# [Conference]: 
# (MSR 2020 Technical Papers)

>Venue: Mon 29 Jun 2020 12:00 - 12:10 at MSR:Zoom - Code Smells 
>>Chair(s): Alessandro Garcia


# ABSTRACT

The boom of the online game market, the huge percentage of video games focused on cellular gadgets or streaming services, and the increasing complexity of video video games cause the provision of video gamespecific gear to evaluate overall performance and maintainability problems.
This paper proposes Unity Linter, a static evaluation device that support Unity online game builders to hit upon seven varieties of terrible smells we've got diagnosed as applicable in online game development. Such scent sorts pertain to overall performance, maintainability and incorrect conduct problems. After having described the smells via way of means of analyzing the prevailing literature and dialogue forums, we've got assessed their relevance with a survey related to sixty eight participants. Then, we have analyzed the incidence of the studied smells in a hundred opensource Unity projects, and additionally assessed UnityLinter’s accuracy.
Results of our empirical research imply that builders wellreceived overall performance- and conduct-associated troubles, at the same time as some maintainability troubles are greater controversial. UnityLinter is, in general, correct sufficient in detecting smells (86%-a hundred% precision and 50%-a hundred% recall), and our examine suggests that the studied scent sorts arise in 39%-97% of the analyzed project.

# 1 INTRODUCTION

Video video games constitute a conspicuous and growing percentage of the software program improvement marketplace. In 2018, the online game industry has generated 134.nine billion dollars, with over 10% growth over 2017 [25]. Such a marketplace is converting constantly additionally in phrases of
systems on which video video games are deployed. In the past, video games in particular focused consoles and computer computers; nowadays cellular gadgets account for almost 1/2 of of the marketplace [24], and the modern-day fashion is the streaming of online game contents.
While the online game marketplace is growing, improvement capabilities in this place nonetheless constitute a niche. Just to provide an idea, Stack Overflow capabilities over 1.5M discussions tagged [java] and 1.2M tagged Android, at the same time as most effective 50k are approximately Unity3D. It is consequently clean how in this context builders might also additionally want appropriate assist at the same time as creating their video video games, assisting them to keep away from introducing overall performance bottlenecks, or making the sport hard to keep and evolve.

Static code evaluation equipment (SCAT) are a normal assist builders have at the same time as coding. Such equipment, recognised additionally as “linters” (from the first device advanced through Johnson for the C language [28]) examine the supply code or the compiled (e.G., bytecode) application to highlight numerous problems. These include, amongst others, in all likelihood bugs (e.G.kind conversions, or doubtlessly incorrect operators implemented to sure types), overall performance issues (e.G., use of programming constructs
which are recognised to be inefficient), safety vulnerabilities, or coding fashion issues (e.G., insufficient commenting or desire of identifiers).
The use of SCAT in software program improvement has been investigated through numerous research. For example, Johnson et al. [27] and Beller et al. [18] have studied using static evaluation equipment in software program tasks.
Other research targeted on investigating the quantity to which such equipment may be used to locate actual faults [45, 48, 50], or how they are utilized in non-stop integration pipelines [49]. Many SCAT are general-purpose, e.G., FindBugs [5], PMD [7] or CheckStyle [4] for Java, Rubocop [1] for Ruby, or Splint [22] for C. Others examine particular sorts of applications, e.G., Android Lint [2] detects Android-particular issues.

In this paper, we recommend UnityLinter, a linter for video video games advanced with Unity [10]. While there are numerous different online game improvement frameworks (e.G., Unreal [11] or Blender [3]), we have selected Unity due to the fact it's miles free (inside sure utilization limits) and for this reason, it has additionally been followed withinside the open-supply community in addition to for academic purposes. UnityLinter statically analyzes the supply code (written in C#) and different artifacts of a Unity video video games, and may locate 7 sorts of online game code smells. Such smells cowl special excellent components of online game improvement,
specifically overall performance, maintainability, and accurate behavior.
We first elicited a hard and fast of 6 smells, through reading present literature on online game design [38, 40], through discussing with experts, and through reading discussions on forums. Then, we surveyed sixty eight video sport builders and accumulated their notion and remarks approximately the smells we desired to locate. This additionally helped us to refine the
odor detection regulations and to locate an extra odor over the 6 we to start with conceived. Finally, we analyzed one hundred Unity open supply tasks hosted on GitHub, so as to (i) locate smells and consequently check the importance of the investigated phenomenon, and (ii) manually validate a statistically consultant pattern of 420 smells to assess UnityLinter’s precision, and check out 5 entire video
video games to assess UnityLinter’s recall.
Results of the observe imply that, overall, builders nicely understand the smells we defined, in particular, the ones associated with overall performance and sport behavior, at the same time as maintenance-associated smells are greater controversial. Our guide validation suggests that UnityLinter achieves, for the special odor types, 86%-one hundred% precision and 50%-one hundred% recall. Depending at the kind, the presence of the studied smells withinside the analyzed tasks varies among 39% and 97% of the
analyzed tasks.
The contribution of this paper may be summarized as follows:

(1) we outline 7 sorts of horrific smells that could arise in online game improvement established via a observe;

(2) we recommend UnityLinter, a linter for video video games advanced in Unity;

(3) we file the effects of a observe assessing the diffuseness of the studied smells, in the accuracy restrict of UnityLinter;

(4) we make the dataset of the observe available [19]. 
Upon acceptance, we additionally plan to launch the device as open-supply.

# 2 BACKGROUND NOTIONS ABOUT UNITY

This phase gives a short creation to Unity, to allow the reader
well information the principles added at some stage in the
paper. Fig. 1-a suggests a screenshot of the Unity improvement environment. A Unity undertaking can both be a 2D or 3-d undertaking (withinside the following we can especially display examples for 3-d projects, as 2D is frequently a subset of 3-d) composed of 1 or greater scenes. A scene describes an interplay area, e.G., a bit of the sport global wherein a participant interacts with different objects. The scene, in turn, carries GameObjects which might be instantiated both statically or dynamically. In our example, the undertaking consists of a scene SampleScene, whose item hierarchy is seen at the left-facet pane of the IDE. More specifically, a scene
carries a camera (Main Camera), that is the angle from
which the consumer sees the scene, a light (Directional Light), and a Cube item (additionally seen on the middle of the screen).
Other than the use of the standard extension mechanisms of objectoriented (OO) programming, Unity permits builders to decorate an item with numerous forms of components, that may be seen on the right-facet pane (i.E., the Inspector). More specifically, an item has a default belongings named transform, which specifies the item position, rotation, and scaling, and different components, e.G., a collider
that handles collisions with different objects, a material (in our case named MyColor) that specifies the item’s visible aspect. Last, however
now no longer least, it's miles feasible to feature one or greater scripts to specify conduct.

In our case, the dice has connected a script named Move Cube (whose content material is proven in Fig. 1-b).
Unity’s conduct is targeted the use of scripts written in C#1. A
applicable magnificence in Unity is MonoBehaviour, and C# training connected to GameObjects inherit from MonoBehaviour. A Unity walking undertaking works as a loop. First, the Start() approach of all MonoBehaviour training connected to GameObjects is executed. Then, the Update() approach is known as in every body. Note that Unity functions versions of Start () and Update() (all blanketed via way of means of UnityLinter), known as at distinctive time, e.G., Awake () is just like Start(),
however is known as whilst a script is loaded, at the same time as the LateUpdate() techniques are known as in the end Update() techniques had been invoked.
FixedUpdate() is invoked with a set frequency, i.E., it does now no longer rely on the body rate.
In the script proven in Fig. 1-b, the Start() approach receives the connection with an aspect of kind Material connected to the dice. By converting one in all its properties, the dice colour is modified upon loading the scene. In every body (Update() approach), a rotation of one diploma over the z-axis is carried out to the dice. Besides rotating the
dice, the Update() additionally dynamically instantiates some other item (a bullet) the use of the Instantiate approach. In this case, the connection with the GameObject isn't always to be had withinside the code however, rather, the item is loaded from a prefab. In Unity a prefab is a reusable asset (commonly a GameObject or a composition of GameObjects with different connected components) saved in a .Prefab file. A developer can create a prefab via way of means of without a doubt dragging a GameObject from an undertaking’s hierarchy to the undertaking resources (decrease pane).

# 3 ELICITATION OF RELEVANT VIDEO GAME SMELLS

While it isn't always an aim of this paper to discover any viable scent that
ought to have an effect on a Unity online game, earlier than imposing UnityLinter we carried out a small research to decide what sorts of smells to detect. To this aim, we depended on more than one reassets. Specifically we (i) mentioned our aim with specialists in online game improvement, (ii) depended on the content material of a few textbooks [38, 40], highlighting proper practices and styles in online game improvement,
and, finally, (iii) we leveraged casual information from discussion boards, particularly the Unity Forum, a few Reddit channels associated to video video games and different Unity improvement boards. In particular, to mine ability scent-associated discussions, we done a seek on the boards the use of the subsequent keywords: (i) “proper practices”, (ii) “awful practices” and (iii) “not unusualplace mistakes”. On the Unity Forum, we analyzed discussions withinside the “support” and “community” sections. The former collects Unity legit manuals, the latter functions questions from the developers’ community. Besides discussions partially regarding viable awful practices, we discovered 29 pages (suggested in the web appendix), amongst the ones withinside the Unity Forum and Reddit, in particular concentrated on awful practices in Unity improvement. 
Based at the numerous reassets of records, we discovered the subsequent troubles being mentioned via way of means of developers, and additionally mentioned in online game layout books:

• The use of Find strategies in runtime code, and, in general,
operations on string literals;

• Instantiating and destroying sport gadgets too often;

• The presence of performance-in depth obligations in Update()
loops;

• Frame price now no longer well taken under consideration whilst scripting good judgment or animation;

• The use of public worldwide variables, affecting records
hiding; and

• Lack of separation of concerns, i.E., developing incohesive
scripts with too many responsibilities.

Based on such considerations, we described 6 scent types. This
preference has been pushed via way of means of one of a kind factors: (i) want to manage with troubles which might be precise to Unity and video video games, and now no longer with time-honored issues, inclusive of loss of records hiding, that might have an effect on any software program project; (ii) functionality to outline a heuristic to detect
the scent statically, although the detection is approximate; and (iii) thinking about smells that cowl a selection of various sorts of symptoms Unity initiatives ought to exhibit.

In the subsequent, we in short describe the 6 sorts of smells we have identified. We categorize them consistent with their negative impact they'll cause, i.E., on performance, maintainability and
behavior.

# 3.1 Performance Smells

Allocating and destroying GameObjects in updates. In Unity,
GameObjects may be allotted statically, i.E., dragging them in the scene hierarchy thru the IDE, or dynamically, i.E., instantiating them the usage of the Instantiate as defined in Section 2. When items are now not needed, they can be destroyed the usage of the Destroy approach. Both Instantiate and Destroy are computationally expensive, and their use in Update () approach may have an effect on the sport performances. If the sport calls for to allocate and wreck many items at runtime (e.G., bullets in a taking pictures game) it's far recommended to use an item pool. In different words, a pool of GameObjects is allotted at runtime and, whilst required, GameObjects are retrieved from the pool and disposed there whilst now not needed. The supply code in Fig. 1-b reveals the defined smell, because the bullet is dynamically load and instantiated at each frame.

Getting a GameObject reference locating it through name. In Unity, a GameObject ought to receives the reference of some other one through searching it through name. In the instance of Fig. 1-a, a GameObject ought to get the reference of the Cube the usage of the instruction:GameObject. Find ("Cube")  This get right of entry to approach is discouraged as it impacts performances.

A comparable problem (FindViewById) is thought additionally in Android [47]. Therefore, it's far foremost to keep away from this reference mechanism, and get get right of entry to to different items thru express dependencies instead.

Heavyweight Update strategies. Since all Update () strategies are invoked at each frame, acting computationally-in depth operations in such strategies may negatively have an effect on performances. Sometimes that is simply unavoidable; however, whilst possible, it's far recommended to aspect out computations that don't require to be executed
each time, shifting them.


# 3.2 Maintainability Smells

Lack of separation of concerns. A MonoBehaviour script that
implements on the equal time unique duties makes the
tasks tough to evolve. For example, allow us to believe that a
GameObject implements a participant (e.G., someone taking walks in an open world). A common mistake is to enforce all of the common sense of the participant withinside the equal MonoBehaviour script, i.E., getting the inputs from the controller, figuring out the item nation (e.G., “can walk”, “can jump”, “can fire”, etc.), and shifting the GameObject. It is advisable, instead, to component out enter managing in a separate elegance hierarchy (using a Strategy layout pattern) in order that the supply code connected to the
participant item does now no longer ought to extrade if, for example, one desires to enforce an synthetic intelligence-dealt with participant. Similarly, the nation control and the participant animation ought to be dealt with in separate scripts.

Coupling objects through the IDE Inspector In Unity, it's miles feasible to couple a MonoBehavior script to different gadgets via the IDE. This works as follows. If a script announces public fields, or private/blanketed fields with the [SerializedField] attribute,such fields will seem as script houses withinside the Unity inspector. Then, from the IDE, the developer can simply drag gadgets into such houses to create a coupling. In the instance of Fig. 2-b, the MonoBehaviour script has two [SerializedField] attributes, mySphere and myCharacter. As proven in Fig. 2-a, each seem as houses withinside the inspector (proper pane). Since the developer has dragged the Sphere into the property, the latter seems crammed with a hyperlink to the Sphere item. Instead, there's no item connected to the myCharacter property.

The predominant poor impact of this programming exercise is the
loss of understandability, i.E., couplings will now no longer be seen from the supply code, however simplest from the Inspector. Much worse, if a developer edits the supply code, or renames scripts or gadgets, couplings are lost, and that they want to be restored manually. There are options to this, consisting of using a messaging device to couple unique gadgets withinside the game. However, such options would possibly be, in some cases, sub-premier for what issues performances.

# 3.3 Behavioral Smells

Animation speed depends on the frame rate If a script plays a translation, rotation, or scaling of a set significance to an item in an Update method, this type of transformation is repeated at each body. As a result, the animation is probably greater or less speedy relying at the body price. This odor is likewise glaring in the Sphere translation of Fig. 2-b. To keep away from the odor, a standard solution followed is to multiply the significance through Time.DeltaTime, which returns the delta time among next frames. In other words, the supply code in Fig. 2-b becomes:
                            
            mySphere.Transform.Translate(0f, 0f,
                    1f*Time.DeltaTime);
In this type of way, the animation velocity can be impartial of the body price.And methods to keep away from or mitigate the odor. Then, we ask to offer a relevance rating in a 5-stage Likert scale [41]. Finally, for every query, the respondent ought to upload an non-compulsory open comment. An instance of query for the odor “Allocating and destroying GameObjects in updates” is suggested in Fig. 3.

• A very last segment with questions on the general, perceived
usefulness of a Unity linter, i.E., (i) whether or not they understand the provision of this type of device useful, and (ii) whether or not they might be inclined to undertake it (note: someone ought to understand it as useful, however now no longer for her/him, only for a few classes of users, e.G., junior developers). Finally, we ask to offer free
feedback approximately feasible smells the respondent understand as pplicable however that turned into now no longer taken into consideration in our study.

To recruit participants, we published the questionnaire on Reddit channels associated with video video games and Unity development, namely gamedev and unity3d. When we published the questionnaire, we added a brief message explaining its purpose, the envisioned duration (10- 15 min.) and a message telling that we might handiest use the collected
statistics in aggregated, anonymized shape.

We file the effects of RQ1 through displaying the perceived relevance in shape of diverging stacked bar charts. We additionally speak the open feedback made through the respondents.

# 4 SMELL RELEVANCE ASSESSMENT

After having identified possible bad smells to detect, we wanted to investigate whether they are considered as relevant by developers, and possibly worthwhile of being addressed. Therefore, we address our first research question:

    RQ1: To what extent are the considered bad smells relevant for video game developers?

# 4.1 Relevance Assessment Methodology

To address RQ1, we behavior a survey with professionals in video game improvement. The survey consists of 5 sections:

• A first phase, in which demographic statistics approximately respondents is collected. More specifically, we requested approximately: (i) the area wherein they work; (ii) their function withinside the organization (e.G., developer, assignment manager); (iii) the years of revel in in software program improvement; and (iv) greater specifically, the years of revel in in improvement with Unity.

• Three sections wherein we ask builders to offer their
perceived relevance approximately smells associated with Performance, Maintainability, and Behavior. For every smell, we offer a short description of the problem, outlining its consequencesand methods to keep away from or mitigate the smell. Then, we ask to offer a relevance rating in a 5-degree Likert scale [41]. Finally, for every query, the respondent ought to upload an optionally available open
comment. An instance of query for the smell “Allocating
and destroying GameObjects in updates” is said in Fig. 3.

• A very last phase with questions on the general, perceived
usefulness of a Unity linter, i.E., (i) whether or not they understand the provision of any such device useful, and (ii) whether or not they might be inclined to undertake it (note: someone ought to understand it as useful, however now no longer for her/him, only for a few classes of users, e.G., junior builders). Finally, we ask to offer free remarks approximately viable smells the respondent understand as applicable however that become now no longer taken into consideration in our study.

To recruit participants, we published the questionnaire on Reddit channels associated with video video games and Unity improvement, namely gamedev and unity3d. When we published the questionnaire, we added a quick message explaining its purpose, the predicted duration (10- 15 min.) and a message telling that we might handiest use the collected records in aggregated, anonymized shape.

We file the outcomes of RQ1 through displaying the perceived relevance in shape of diverging stacked bar charts. We additionally speak the open remarks made through the respondents.

# 4.2 RQ1: Relevance Assessment Results

After weeks of retaining the survey open, we received a complete of sixty eight responses. 26 respondents had much less than five years of improvement experience, 26 among five and 10 years, and 15 greater than 10. About Unity, forty seven respondents had much less than five years of experience, 19 among five and 10, and 1 greater than 10. One did now no longer offer any answer to demographic information. Most of the respondents (61) had been expert builders, except three product owners, 2 students, and one manager. In phrases of improvement domain (more than one solutions allowed), maximum of the solutions noted “Video sport improvement” (48) and Virtual reality (15). Others consist of well-known software program improvement/consulting (6), pc portraits (4), content material platform provider (three), or clinical software program (2). Table 1 reports, withinside the shape of diverging stacked bar charts the perceived relevance of the 6 scent types. The 3 percentages proven withinside the graph suggest the percentage of disagreements, impartial responses, and agreements respectively. Also, dark/mild green suggests the percentage of “Strongly agree” and “Agree” responses, while dark/mild brown suggests the percentage of “Strongly
disagree” and “Disagree” responses.

# Allocating and destroying GameObjects in updates. 

Respondents commonly agree (79% of fine solutions) approximately the usefulness of the use of item swimming pools rather than allocating/destroying in Update() methods. At the identical time, a few respondents had been impartial or maybe disagreed. For a number of them, the item pool can also additionally eveni ntroduce insects withinside the implementation, while others indicatedthis is a superb practice, however they practice it best in which the specific
implementation calls for it. In different words, an occasional allocation/spoil is acceptable, while a huge allocation/destructionof items makes the item pool worthwhile. Also, pool length and allocation frequency create a trade-off among the use of the pool or now no longer, due to the fact a massive pool would possibly bring about a waste of allotted memory. Finally, one respondent noted how the greater latest C#
runtime makes rubbish collection (activated upon Destroy) greater green than before.

# Heavyweight Update methods.

In this case, 82% of the respondents agree approximately the scent. At the identical time, in addition they suggest that(i) as expected, a right evaluation of this scent calls for a run-time profiler, (ii) Unity handles lengthy name stacks quite well, (iii) nested loops can be an amazing indicator of ability problems, however best whilst the extent of nesting is over three-4. Finally, respondents endorse the use of coroutines (a Unity mechanism for multi-threaded execution) to
alleviate this problem.

# Getting a GameObject reference finding it by name. 

Almost all respondents (91%) suggest that the usage of Find is a bad practice. Besides performance-associated effects, Find additionally makes the supply code fragile in case someone renames items. One respondent indicated that the usage of Find can nonetheless be an amazing practice whilst retrieving a reference in an item hierarchy (for example, retrieving the connection with the top in a humanoid version from the upper-degree box item). Respondents advocated creating
coupling thru the inspector, instead.


# Lack of separation of concerns. 

Respondents commonly agree (66%) approximately the usefulness of setting apart concerns. However, thereis a vast percentage (24%) of impartial responses, in which respondents additionally said “It depends”, bringing up that an immoderate fragmentation of obligations in more than one MonoBehaviour scripts can also additionally bring about a waste of effort, code greater hard to be understood,and, above all, it is able to negatively have an effect on performances.

# Coupling objects through the IDE Inspector.
This is the maximum arguable of our smells: 31% of fine responses, 34% negative, and 35% of impartial. While respondents agree that an immoderate degree of coupling makes the venture hard to maintain,coupling thru the inspector has severa advantages. First, it's far higher than different solutions (use of Find or messaging systems) in phrases of performances. Second, it is straightforward to apply even for
non-programmers (e.G., portraits experts) that take part withinside the improvement. Third, it's far beneficial for the duration of checking out activities, because it allows builders to attach/detach items.

# Animation speed depends on the frame rate. 

There is a standard agreement (91% of superb solutions) on this case. At the identical time, respondents suggest that now no longer most effective Time.DeltaTimeought to be used to scale transforms and cause them to body rateindependent but, additionally, to carry out transforms interior FixedUpdate() in place of Update(). While Update() is completed as soon as in keeping with body,FixedUpdate() execution frequency relies upon at the body rate and, for this reason, could now no longer appearance quicker or slower.

Fig. 4 shows, once more withinside the shape of diverging stacked bar charts, consequences associated with the perceived usefulness of UnityLinter, and whether the respondent could use it if to be had as a device. 64% of the respondents agreed approximately the usefulness of a UnityLinter, even as most effective 51%indicated that they could use it if to be had as a device. We conjecturedthat responses to those solutions should rely on the respondents’ improvement experience (standard and, in particular, with Unity). We checked this courting the use of permutation tests [16] (nonparametric opportunity to the Analysis of Variance), and we found no sizable consequences, i.E., the consumer notion of UnityLinter’s usefulness, and the willingness to undertake it as a device do now no longer rely on
the developers’ experience.

Finally, respondents furnished a few recommendations for in addition odor detection. These include:

(1) Analysis of naming conventions. Note that, inside proper
limits, that is to be had for language like Java (e.G., with CheckStyle) and in standard plenty of studies in this subject matter has been carried out [12, 31].

(2) User interface-associated smells.

(3) Lack of caching while the use of GetComponent().

(4) Empty techniques in MonoBehaviour classes (generated with the aid of using the IDE) that motive pointless delays.

Interestingly, respondents additionally talked about how lots of the Unity tutorials incorporate smells the various ones we advise and, i standard, code respondents agree with to be smelly.
While recommendations (1) and (2) are out of scope for thiwork, we accompanied up on suggestion (3) accounting for it while imposing the Getting a GameObject reference locating it with the aid of using name, and (four) with the aid of using imposing a 7th odor detector, i.E., A MonoBehaviour class carries empty techniques.

    RQ1 Summary: Developers generally agree about the usefulness of defecting performance-related issues, although they point out that only the excessive use of such practice might produce visible problems. Maintainability issues are less of a concern when the price to pay is reduced performance.

# 5 UNITY LINTER - ARCHITECTURE AND IMPLEMENTATION 

In this section we describe UnityLinter, a static analysis tool able to recognize 7 Unity smells, i.e., the 6 described in Section 3, plus the A MonoBehaviour class contains empty methods. UnityLinter has been developed as Python scripts, which takes as input a Unity project and, before detecting smells, extracts three pieces of information: (1) A parse tree of C# files using the srcML tool [21]. (2) A call graph using Doxygen [30]. Doxygen generates documentation starting from the source code. For this purpose, it is able to extract call graphs, inheritance diagrams, and collaboration diagrams. (3) Data flow information using srcSlice [13, 39]. After having extracted the parse tree, call graph, and data flow, we leverage them to identify the smells, using the rules described in the following.

# 5.1 Detection Rules

This phase ambitions to element the detection policies described for every odor.

# Allocating and destroying GameObjects in updates.: 

to detect this odor UnityLinter leverages the decision graph extracted via way of means of Doxygen.Basically, we look for the presence of Instantiate and Destroy invocations both in Update() strategies, or in strategies transitively known as via way of means of Update(), in step with the Doxygen name graph.

# Getting a GameObject reference finding it by name: 

the detection of this odor is tremendously straight-ahead and comparable to the preceding one, in that we search for the presence of Find-associated invocations in Update() strategies, or in strategies accessible from Update(). Based additionally at the comments we acquired withinside the survey of Section 4, the invocations we healthy are Find, FindWithTag, FindGameObjectWithTag, and GetComponent.

# Coupling items through the IDE Inspector: 

we examine parse bushes produced via way of means of srcML, figuring out the presence of public or [SerializeField] fields of kind GameObjects or different nonprimitive types. These constitute fields wherein the developer normally drags GameObjects to create static couplings. We discard primitive kind fields due to the fact those are normally used to set constants and different houses via the Unity Inspector. Then, to test whether or not a script is, certainly related to a scene (i.E., in any of its GameObjects), UnityLinter retrieves its identifier (guid) in its metadata record generated via way of means of Unity. Then, it tests whether or not the guidis in any scene metadata.


# Heavyweight Update methods: 

statically-figuring out computationally-in depth strategies is especially challenging, as this challenge is regularly done via a profiler (Unity affords a pretty thorough profiling infrastructure). Nevertheless, it could be beneficial to early warn builders at the same time as writing source
code. To this aim, we search for signs of capability heavyweightUpdate() strategies. More specifically, we search for 3 different varieties of signs: (i) a excessive diploma of nesting in loops; (ii) an immoderate quantity of technique calls; and (iii) the presence of Unity API invocations recognised to be especially high priced.

For the primary cases, a threshold ought to be set. While a developer should pick herself a way to calibrate such thresholds, the technique we comply with to set thresholds in our analyses (and withinside the studypronounced in Section 6) is to take into account as heavyweight all Update() strategies having loop stage of nesting or quantity of technique calls
exceeding the 0.33 quartile of all Update() strategies withinside the project. In the absence of ancient facts, one should set those thresholds primarily based totally on preceding enjoy or facts from different projects.
For the 0.33 case, we take into account high priced APIs documented in Unity-associated forums [6]. In the cutting-edge implementation, the taken into consideration APIs are associated with the Camera.fundamental access, and tomessaging, i.E.,SendMessage and BroadcastMessage.

# A MonoBehaviour class contains empty methods:

we enforce this odor via way of means of surely checking for the presence of empty Start() and Update() strategies in MonoBehaviour classes.

# Lack of separation of concerns: 

this odor can be associated with numerous components of software program improvement and, in our context, of Unity improvement. While one opportunity might have been to leverage conventional methods aimed toward computing loss of brotherly love (for example, via way of means of computing the conceptual brotherly love metric [36]), we observed that this will now no longer paintings nicely in our case. For example, a technique should comprise an invocation to an item rework and any other one converting the item kingdom or gaining access to a controller.
Therefore, we opted for enforcing a totally precise case of detector capable of pick out MonoBehaviour scripts containing each access to GameObject.rework and to the Input elegance, 
i.E the only chargeable for dealing with enter controllers.

# Animation speed depends on the frame rate:

this odor occurs whilst the significance of a GameObject rework isn't always scaled using Time.DeltaTime, i.E., whilst it does now no longer account for the body rate.
A easy detection should test the presence of Time.DeltaTime in
rework operation parameters. However, the rework should additionall get different variables described as a feature Time.DeltaTime. To this aim, we leverage srcSlice to test for the presence of def-use chains among variable definitions and rework calls. If a rework name does now no longer comprise any Time.DeltaTime reference, nor (transitively) makes use of variables described on Time.DeltaTime, then we spotlight the
odor.
