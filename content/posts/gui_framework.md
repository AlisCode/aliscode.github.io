+++
title = "A game-oriented GUI framework"
description = "Building an open-source GUI Framework for game engines"
date = 2021-02-26
draft = true

[taxonomies]
tags = ["Rust", "GUI", "Game Engine"]
+++

# Introduction

# Writing the UI of your game in Rust 

To put it simply (keep in mind that this post is focused on GUI, not on being an exhaustive Rust gamedev tour), the "Rust Gamedev ecosystem" looks like this : 

{% mermaid() %}
graph TD
    ECS[ECS-Based] --> B[bevy]
    ECS --> A[amethyst]
    F[Freestyle] --> M[macroquad]
    F --> G[ggez]
    F --> P[piston]
    F --> C[coffee]
{% end %}

(See [arewegameyet.rs](https://arewegameyet.rs/) for a full tour of the ecosystem.)

Let's start with the "Freestylers". What do those have in common ? They're a pack of all things you need to write a game, glued together so you have everything in one place. They will provide a basic framework for you to work with, and let you handle the specifics yourself. They leave you mostly free. 
* `ggez` is a small-ish game engine inspired by `Löve`, that's aimed at making a small game.  UI-wise, it has capabilities to render a UI but will let you do all the dirty work yourself. No layout, only text and primitives rendering. 
* `piston` is one of the first game engines in Rust. It's not very actively developed anymore. I see it as a mere proof of concept for Rust game engines. What's interesting about it UI-wise is `Conrod`, the UI system they developed for it. It was meant (with modularity in mind) to be integrated in any render pipeline, and it is Immediate-mode.
* `coffee` is a very interesting one. At this point the project is on pause, but it's from that game engine that the well-known `iced` project has emerged. The UI pattern is meant to follow [the Elm architecture](https://guide.elm-lang.org/architecture/). It's pretty elegant, UI-wise, but we'll get later to what I think its limitations are. 
* Last but not least, `macroquad` is a game engine with a clear focus on the web. It has embedded [`megaui`](https://github.com/not-fl3/megaui), an Immediate-mode GUI framework (made by the same author). 

The more popular alternatives are `bevy` and `amethyst`, ECS-based game engines[^ecs]. They will handle everything for you, from the game loop to handling the user input, and will only let you specify your game logic. I personally prefer this approach to the more "Freestyle-ish" one, because I think that ECS and Data-driven design is a great fit with Rust. The former has built a community with a lot of momentum during the last year, and has a focus on simplicity. The latter is the pioneer of ECS in Rust game engines, actively developed, and aimed at becoming a professional-grade engine, meaning it is of course more complex, but try as much as possible to avoid compromising sacrosanct performances.

Both engines have developed their in-house UI solutions. They are meant to play well with the framework. While Amethyst's UI framework has quite a lot more features than the other as of writing, both engines have a focus on modularity, meaning it's [possible](https://github.com/mvlabat/bevy_egui) [to write](https://github.com/mvlabat/bevy_megaui) your own UI implementation for those. Namely, I've taken it upon myself to write [an Iced backend for Amethyst](https://github.com/amethyst/amethyst_iced) (or what it might look like, with more work).  

So, what do we learn from all this ? Well, it seems that every engine has its own solution to solve the very complex problem that UI is. The thing is, those solutions are often meant with a specific use-case in mind, that is, the design of the game engine. They strongly couple your UI code to the engine, for better or worse. And you can't really benefit from other people's work because of **that lack of modularity**. 

In my opinion, the only GUI framework that *used* to get this right was `Iced`. But the project has turned into a general-case GUI framework (understandable, given the context of its development). And if you don't like the Elm architecture, you were always goint to be out of luck anyway. 

# The specific case of games   

* What is needed for a game UI ?
* What the Rust UI frameworks got wrong 

# Core values of a Game UI Framework 

* Modularity
    * Don't be smart
* Performance
* Data-driven
* Focus on animation 

# Conclusion

--- 

[^ecs] ECS stands for Entity-Component-System, covering what those are is out of the scope of this article.