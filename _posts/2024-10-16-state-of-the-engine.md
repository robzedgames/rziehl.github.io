---
layout: post
category: coding
subtitle: And Drawing Lines In The Sand
---

I have been working on the same side project for three years now (although bits and pieces date back later than that) and I feel like it's a good time to reflect on how far I have come and what the next steps are.

Here's some rough metrics [^1] for the current codebase:

* **24722** lines of code (actual source lines, not whitespace or comments) [^2]
* **2895** comments
* **379** todos
* **5926** lines of JSON data [^3]

> *Full disclosure: I am coding my game engine from scratch using [SDL2](https://www.libsdl.org/) and C++ as the foundation. I opted not to use a commercially available engine like Unity or Unreal for my game.* [^4]

This could still be [a more time consuming approach](https://moonstoneequation.com/a-warning-to-others/) but honestly I find it more productive. However, the age old question of *"are you making a game or an engine?"* still comes to mind. As a programmer first, it's easy to get wrapped up in coding neat little technical details and systems. I am definitely guilty of this.

Now though, I need to realistically focus on the game itself.

---

I think while I have a lot of the systems in place or at least rough versions of them, a pragmatic line in the sand would be the difference between production ready technical aspects and actual gameplay. Production ready things would include handling integrated versus dedicated GPUs, UTF-8 support, a full featured settings screen, remapping controls, high DPI support, achievements and testing different CPU architectures.

My core focus now will be to get something playable and fun. Then I think I will extend that prototype to the first vertical slice and polishing that as much as possible. This is an exercise that the developers of Hollow Knight, Team Cherry did. It helps set the standard for what the rest of the game should look like plus it also makes
a good cut-off point for a demo (which I think is becoming more and more important with Steam Next Fest being a key marketing opportunity for indies).

After that I will begin roughing out the rest of the world and making the story playable from beginning to end.
Then probably some rounds of polish, playtesting and finally all those production ready criteria mentioned above (as well as any optimizations that are needed).

---

As of today this is quick overview of some of the main systems in my engine:

* **AI**: Behaviour trees. Needs unit testing to iron out any edge case bugs but otherwise it's dangerous enough to make something functional as demonstrated with the first creature in the game. Pathfinding needs to be implemented still.
* **Animation**: Frame based animations implemented with different frame lengths supported as well as events that can be triggered on specific frames which helps
for playing sounds and actually doing certain behaviours.
* **Audio**: There is a basic engine done with Fmod. Still needs panning and fading over time effects, some basic 2d location for sound would be nice to have too.
* **Collision**: Basic bounding box checks for now, will need some work for sure especially with some of the more physics based entities.
* **Cutscenes**: Mostly there, a few events still needed and some bugs need to be worked out.
* **ECS**: Custom solution, using it more as an organizational pattern as opposed to an optimization one right now. Quite a lot of components already completed, proving to be quite reusable.
* **Input**: Very simple implementation right now. Needs controller support and maybe a more data-driven approach to which actions get triggered in what context.
* **Map Editor**: Very early stages. Missing a lot of functionality.
* **Message Queue**: Decent implementation that can be used across broader systems. Ability to add additional information with a message would be nice.
* **Rendering**: Mostly good. Water rendering will need to be implemented properly and particle systems need to be finished. Lighting is pretty much done though.
* **Resource Loading**: Pretty good system in place. I have a side project to make this even more data driven so I can really simplify all the serialization code.
* **Saves**: Entities get saved properly for the most part. Map changes do not as well as some other game state.
* **Tests**: I think there’s a basic test runner and maybe some of the math tests but otherwise severely lacking.
* **UI Framework**: Mostly there. Dropdowns, scrollbars and text inputs all need some fixes. Multiline paragraphs still haven't been implemented.

So not a bad base overall, it could be better, there's lots of gaps as my spare time has been dedicated to this very sporadically. Work and life gets in the way and sometimes my attention shifts around. But I think it's enough to whip up a prototype so that's my turning point from initial engine to more actual gameplay. On rainy days when I need a break from my current task list I might pick something engine related to improve or maybe work on some dev tools (like an in-game console, hot reloading or a debug view). They might speed up development in some situations and be worth the additional effort.

---

So why write this post? It's mostly for myself. I'm taking a snapshot at this point in the development of this game to come back to years later for perspective. I'm sure that I'll change my mind on some of these thoughts over time with but let's see.

I am really curious to see by the end of this project, years from now, what the metrics will look like. I find posts like [this one](https://kotaku.com/the-exceptional-beauty-of-doom-3s-source-code-5975610) great for providing some similar stats. 

> *To put things into perspective: Dyad has 193k lines of code, all C++. Doom 3 has 601k, Quake III has 229k and Quake II has 136k. That puts Dyad somewhere in between Quake II and Quake III. These are large projects.*

Dwarf Fortress is supposedly [700K LOC](https://stackoverflow.blog/2021/12/31/700000-lines-of-code-20-years-and-one-developer-how-dwarf-fortress-is-built/). [^5]

These are by no means an objective level of quality or perfection but they are fun to indulge in from time to time.

---

In the next post, I want to continue this chain of thought and talk about actually building out a game idea.

---

[^1]: Metrics were generated with `sloc` && `wc -l *.json`
[^2]: This also excludes all open source dependencies
[^3]: The game is fairly data driven although a good chunk of this is a massive map file that features a 2D grid (that'll get optimized over time)
[^4]: Many jobs ago I worked with Unity and had to deal with a few major version upgrades that had breaking changes. Writing my own engine may require more time up front but it's a trade-off so I do not have to invest time continuously whenever new engine updates arrive. Nevermind the ripple effect it has on plugins that you might use that don't get updated as fast too. I also opted not to use Unreal Engine because I am not thrilled with their revenue share model. After Steam's 30% cut, your business taxes and your own personal taxes, adding another fee on top of all that was not particularly appealing.
[^5]: Although Tarn Adams did the metric by searching for `;` characters and not using a tool like `sloc`. However, he coded Dwarf Fortress, we know it's a large codebase. What's an extra 10K lines of code here and there?