---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Julia 1.10
  language: julia
  name: julia-1.10
---

# Chapter 3: Graph Relationships

## Introduction

In the previous section we took a look at directed graphs; what they are, what they can represent, and how we can describe them to a computer. In that chapter we investigated the relationships within a graph. In this chapter, we're going to investigate relationships *between* entire graphs.

Comparing graphs is useful. Suppose there's some situation that we've modeled using a directed graph. If someone else has created a related directed graph we may want to be able to systematically compare it to ours or even merge the two.

But an understanding of graph relationships are also an important thinking tool, and the next step on our journey to relational thinking. We are building up an understanding of graphs and, at each stage, we're paying special attention to the *relationships* that are relevant. Like any abstraction, this may seem a bit pedantic and unnecessary at first. Relational thinking takes time. By the end we will see that there are nice freebies you get when you build up your manner of thinking by focusing on relationships.

## Part 1: Graph Injections

*Informally:*

In what way might two graphs be related? One of the most obvious possibilities is that there may be a copy of one graph inside of the other.

In Chapter 1 we saw an example of a directed graph which described the layout of a ski resort. In this account, you could ride the ski lift up and down the mountain or ski from the top of the mountain into a nearby village.

But suppose we visit this ski resort in the Summer when there's no snow. At this time of year the resort lets guests ride up and down the mountain in the lift (which provides a *lovely* view!), but there is no way to get down the mountain into the village without a snow pack to ski on.

![whoops!](./assets/Ch3/SummerWinter.png)

Note that the Summer graph is basically contained inside of the Winter graph. How should we characterize this relationship?

In the previous chapter we thought about relationships in terms of maps. We can do something similar here. For the Summer graph to be a "part" of the Winter graph means, in effect, that we can map the Summer graph *into* the Winter graph, taking vertices to vertices and arrows to arrows.

![whoops!](./assets/Ch3/InjectionSki.gif)

We call this a "graph injection". In order to visualize injections clearly let's introduce some new visuals.

*Figuratively:*

Let's step away from the ski lodge and look at graph injections more generally. We want to represent the injection of graph 1 into graph 2:
![whoops!](./assets/Ch3/InjectA.png)
First, let's redesign graph 2 to be a "recipient" of the graph 1, moving the colors and shapes out of the way.
![whoops!](./assets/Ch3/InjectB.png)
We now place the first graph inside of the second graph.
![whoops!](./assets/Ch3/InjectC.png)
This gives us an image of "what went where" in our injection. We sometimes call this the "image" of the first graph in the second.

It's important to understand that a graph is not allowed to come apart when getting injected. An arrow must stay attached to its source and target vertices through this process.

![whoops!](./assets/Ch3/DanglingEdge.png)

For modeling purposes, it is the connectivity of the graph that matters. If an injection ruptures the graph this way it would also rupture any underlying meaning we may have ascribed to that graph. DEFINE Dangling edge condition (eg In the ski lodge example, ...?)


### Problems ###

1. How many ways can you inject this upper graph into the lower graph?

![whoops!](./assets/Ch3/Problem1.png)

Answer:

Three! The upper triangle can be injected in any orientation.
![whoops!](./assets/Ch3/Problem1Solution.png)

2. How many ways can you inject this upper graph into the lower graph?
![whoops!](./assets/Ch3/Problem2.png)

Answer:

Twelve?

*Formally:*

In chapter 1 we used source and target maps to describe a directed graph. Maps can also be used to describe an injection. In this case the a “vertex map” and an “arrow map” run vertically, telling where each vertex and arrow ends up in the injection.

![whoops!](./assets/Ch3/A,V,Maps.gif)

These two maps capture all the relevant information about the injection.

Recall our dangling edge condition: For these maps to represent a proper injection the arrows must stay attached to their source and target vertices. Clearly the above maps must work together in some way to prevent breakage. What conditions must be true in order to ensure that a graph doesn't come apart on entry?

To answer this, let's arrange our maps into a square, with the source maps for graph 1 and graph 2 running horizontally and the “arrow map” and “vertex map” running vertically :

![whoops!](./assets/Ch3/CommSquare.gif)

Note how the dashed lines seem to flow “out” from the arrows in the upper left and flow “in” to the vertices at the lower right. Starting from any given arrow there are two paths you can take around this square, an upper route and a lower route. Let's focus on a specific arrow and consider what these routes “mean”. (We'll label the endpoints as "A" and "V")

### Upper Route ###

![whoops!](./assets/Ch3/UpperRoute.gif)

Reading across the top we have that the red arrow has the heart as its source. Reading down the right side we see that the heart gets sent to the square vertex in graph 2. So the square is "the vertex that receives A's source."

### Lower Route ###

![whoops!](./assets/Ch3/LowerRoute.gif)

Reading down the left we have that the red arrow from graph 1 gets sent to the blue arrow from graph 2 (In other words, the blue arrow is its "image"). Reading across the bottom we see that the blue arrow has the square vertex as its source. So the square is "the source of the image of A."

Let's now revisit to our dangling edge condition. “Coming apart” means, literally, that a vertex and an arrow that were connected in graph 1 are not connected when they land in graph 2. Suppose an arrow gets separated from its source by an attempted injection. For that arrow, the two routes around the square look like this:

![whoops!](./assets/Ch3/OpenSquare.gif)

That is, what it “means” for a graph to get broken is precisely that “the vertex that receives A's source” is *different* from “The vertex that is the source of A's image.”

Thus we can actually DEFINE what we mean by a graph injection as a square in which all arrows have closed loops going either way around.

![whoops!](./assets/Ch3/InjectionFadethrough2.gif)

Of course, the same maps must also have closed loops for the arrows and their targets. Together, all of the “data” describing this embedding is caputred in the following diagrams:


![whoops!](./assets/Ch3/FullHomomorphism.gif)

We have defined one thing – graph connectivity in injections – in terms of another thing – closed loops. Imposing the rule that the certain loops must close is called a "commutativity condition".

It turns out there are a lot of ideas that can be captured by connecting maps together and then declaring some commutativity conditions. Commutative diagrams are the bread and butter of category theory. We will not explore the general notion of commutativity in much depth here. For a thorough yet elementary introduction to this topic we recommend Lawvere and Schnual's *Conceptual Mathematics*.

As we'll see, one of the benefits of describing injections and dangling edge conditions in terms of maps is that maps and commutativity conditions are easy for the computer to understand maps and inspect. This allows the computer a way to be of use to us without that computer needing to have any actual understanding ideas like vertices, arrows, attachments..the semantics of graphs.








