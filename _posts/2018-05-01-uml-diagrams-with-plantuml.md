---
layout: post
title: PlantUML
subtitle: UML Diagrams 
bigimg: /img/ricardo-resende-437822-unsplash.png
tags: [visualization, software engineering]
---

I like the dot and Graphviz tools and used it in many projects to visualize complex topics or create overviews. They are easy to do and there is ample of tool support. I did not use UML diagrams (beyond whiteboards) for the same reason.

I recently discovered that the situation changed. PlantUML provides us with decent tooling to get UML diagrams going. I checked for support in IntelliJ, Sphinx, and Jekyll. On top of that PlantUML generates PNG images for universal use.

There are two big points for PlantUML to make it very productive:

* write the diagram in any editor very quickly (i.e. use text files) 
* do not bother tweaking the layout of elements, which makes creating diagrams fast. PlantUML finds the best position of diagram elements for you


Let's have a look! The following snippet shows how a diagram is "programmed" in PlantUML:

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


Here the result:

{% plantuml style="width:30%" %}
[script] -down-> [log]
[script] -down-> [Line]
{% endplantuml %}


I hope this information is helpful to you.

All the best, Mark


## Resources

* [PlantUML](http://plantuml.com/)
* [PlantUML for Jekyll](https://github.com/yegor256/jekyll-plantuml)
* [PlantUML for Sphinx](http://build-me-the-docs-please.readthedocs.io/en/latest/Using_Sphinx/UsingGraphicsAndDiagramsInSphinx.html)
* [PlantUML for IntelliJ](https://plugins.jetbrains.com/plugin/7017-plantuml-integration)
* [Graphviz](https://www.graphviz.org/)
