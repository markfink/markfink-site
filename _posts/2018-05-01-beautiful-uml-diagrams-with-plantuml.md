---
layout: post
title: Beautiful UML Diagrams
subtitle: using PlantUML
bigimg: /img/uml-sample.png
tags: [visualization, software engineering]
---

I like the dot and Graphviz tools and used them in projects to visualize complex situations or to create overviews. These visualizations are easy to make and there is ample of tool support. For many years I did not use UML diagrams (beyond whiteboards) because it was painful.

Recently a coworker indicated that the situation changed. PlantUML provides us with decent tooling to get UML diagrams going. IntelliJ and friends which have fine support for PlantUML. On top of that PlantUML generates SVG / PNG images for universal use.

There are two PlantUML features which make it very productive:

* diagrams can be quickly written in any text editor (by use of text files) 
* no need to bother tweaking the layout of elements - PlantUML finds the best position of diagram elements for you


Let's have a look! The following snippet shows how a diagram is "written" in PlantUML:

{% highlight text %}
@startuml
actor "Main Database" as DB << Application >>

note left of DB
  This actor 
  has a "name with spaces",
  an alias
  and a stereotype 
end note

actor User << Human >>
actor SpecialisedUser
actor Administrator

User <|--- SpecialisedUser
User <|--- Administrator

usecase (Use the application) as (Use) << Main >>
usecase (Configure the application) as (Config)
Use ..> Config : <<includes>>

User --> Use
DB --> Use

Administrator --> Config 

note "This note applies to\nboth actors." as MyNote
MyNote .. Administrator
MyNote .. SpecialisedUser

'  this is a text comment and won't be displayed
AnotherActor ---> (AnotherUseCase)

'  to increase the length of the edges, just add extras dashes, like this:
ThirdActor ----> (LowerCase)

'  The direction of the edge can also be reversed, like this:
(UpperCase) <---- FourthActor

@enduml
{% endhighlight %}


Here the resulting UML diagram:

![PlantUML diagram](/media/plantuml_result.svg)

I hope this information is helpful to you.

All the best, Mark


## Resources

* [PlantUML](http://plantuml.com/)
* [PlantUML for IntelliJ](https://plugins.jetbrains.com/plugin/7017-plantuml-integration)
* [Graphviz](https://www.graphviz.org/)
