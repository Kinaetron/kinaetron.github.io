+++
title = "Moonworks Resources"
date = "2025-06-06T10:36:28+01:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["Moonworks", "Game Development", "Resources"]
keywords = ["Moonworks", "Game Development"]
description = "Resources For Moonworks"
showFullContent = false
readingTime = false
hideComments = false
+++

This article goes over all of the resources available for Moonworks at the time of writing. Please also keep in mind that Evan Hemsley the developer of Moonworks was also one of the main developers of SDL_GPU which the  Moonworks Graphics API pretty much maps to. So there will be a lot of cross over information between the two frameworks.

## Moonworks Graphics Tests

So the author of Moonworks Evan wrote up a nice little project showing new users how to do standard graphics programming operations in Moonworks, such as getting a clear window up, rendering a triangle, rendering a texture and a whole host of other graphics programming examples.

You can download it from [here](https://github.com/MoonsideGames/MoonWorksGraphicsTests/tree/main)


## ROLL AND CASH (GGJ Example Game)

ROLL AND CASH is a game written with Moonworks for the 2024 Global Game Jam. It’s a fairly small and complete example of a game written in the framework in a good way.

You can get the game itself from [here](https://prophetgoddess.itch.io/roll-and-cash-grocery-lords).
You can download the source code [here](https://github.com/thatcosmonaut/GGJ2024).

## Moonside Game Website

 Evan also runs the website https://moonside.games where he posts about graphics articles about Moonworks and SDL GPU, which he also developed

I would specifically point you to these articles on there
- [Shadercross article](https://moonside.games/posts/introducing-sdl-shadercross/), Shadercross being a library that allows you to cross compilation of different shader languages on the backend of the Graphics API that Moonworks / SDL_GPU support.
- [SpriteBatcher article](https://moonside.games/posts/sdl-gpu-sprite-batcher/), which explains how to write a basic SpriteBatcher, a graphics programming technique that allows you to render a large number of sprites at the same time. The article is about applying this technique to SDL_GPU, but it’s pretty much the same in Moonworks and there is an example of the technique in the Moonworks Graphics Tests.
- [Cycling article](https://moonside.games/posts/sdl-gpu-concepts-cycling/), Cycling a concept introduced to the SDL_GPU / Mooworks which is to do with the integrity of the data uploaded from the CPU to the GPU.

## Youtube Videos

- [Glitch City LA ECS Talk](https://www.youtube.com/watch?v=v8OkkHSQjWg). Evan also did a video at Glitch City LA back in 2023 about ECS (Entity Component System) which is a style of game code architecture that most Moonwork projects use and for good reason.
- [How I put a game on Steam with a custom engine in 2 months](https://www.youtube.com/watch?v=YDgiUlXFg3o). [Cassandra Lugo(prophetgoddess)](https://blood.church/) Made a video talking about the advantages of making games without a large game engine. The game she talks about in that video [break.up](http://break.up) was written in Moonworks and she goes into some detail how she accomplishes this in that video.

## Articles
- [Moonworks Setup article](https://kinaetron.github.io/Blog/posts/moonworks-setup/). So I wrote up an article going into detail about how to set up a Moonworks project from scratch.
- [Moonworks Graphics Programming Intro](https://kinaetron.github.io/Blog/posts/moonworks-graphics-intro/). I wrote an article about the basics of graphics programming using Moonworks.
- [Making a simple shoot-em-up with FNA and MoonTools.ECS](https://blood.church/posts/2023-09-25-shmup-tutorial/). Cassandra goes into detail about the basics of making a game using the combination of FNA and Moontools.ECS. This article relies on an older version of Moontools so everything isn’t completely up to date, but it’s a great read nevertheless.
- [SDL_GPU Documentation](https://wiki.libsdl.org/SDL3/CategoryGPU). As I mentioned at the beginning Moonworks Graphics API is pretty much a C# mapping of SDL_GPU so looking through the documentation should help greatly.
- [Mesh rendering with MoonWorks](https://allyourfaultforever.com/posts/sdl3-static-meshes/). Chip Collier wrote a article about rendering a basic mesh in Moonworks.

## Discords

You can also join the discords listed below. Great places to keep up with the latest news, help other users out and ask questions.

- [Moonworks](https://discord.gg/ujhwdkHmhN)
- [SDL](https://discord.com/invite/BwpFGBWsv8)