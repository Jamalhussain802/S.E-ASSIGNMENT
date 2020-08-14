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