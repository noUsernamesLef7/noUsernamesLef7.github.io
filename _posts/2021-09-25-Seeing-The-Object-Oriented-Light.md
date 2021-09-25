---
layout: post
date: 2021-09-25
author: Jason Brown
title: Seeing The Object Oriented Light
---
I recently participated in my first hackathon. I was invited by a friend and we wrote a simple game played via a Discord bot. We called it [Ancient Adventure](), as there was a pre-historic theme to the hackathon. It was  inspired by the old school text adventure games like Zork with a bit of MUD influence. I gained a few valuable insights from the experience and had a blast doing it. I'll probably end up writing a couple of blog posts based on the experience and lessons learned but for now I'm going to write about how the value of object oriented design finally sank in from doing things the wrong way.

Long story short, our game code ended up being messy and the exact opposite of object oriented. Each room in the game was implemented in it's own function, there was basically no code reused between rooms, and there was a tangled mess of if statements that made debugging and testing an exhausting endeavor. We were about halfway through when we realized how difficult the structure was making things but because of the nature of the hackathon, didn't have enough time to re-write it and had to commit.

In hindsight, one of the big changes we should have made was separating out the bot code, the game engine code, and the game content into separate files. The database code I wrote was practically the only thing separated out from the rest of the game. We should have written a class representing all the repeated structures in the game: monsters, items, rooms, characters, etc. This would have saved a lot of time and effort in the initial creation phase, testing, and debugging. It would have allowed us to focus on and greatly expand the content and gameplay. The product suffered and was limited as a direct consequence of us not writing it in an object oriented fashion.

So, while I'm fairly familiar with writing OO code and best practices, it took this experience of doing things completely the wrong way to finally be able to say that I truly understand the need for putting thought into how your code is structured.
