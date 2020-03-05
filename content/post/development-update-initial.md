+++
authors = []
date = 2020-03-04T23:00:00Z
draft = true
excerpt = "In our first sprint, we set up the most important systems of the game, the buildings and the spawning of the enemy minion hordes."
hero = "/images/portals_initial.PNG"
timeToRead = 10
title = "Development update - Initial"

+++
In our first sprint, we set up the most important systems of the game, the creation buildings and the spawning of the enemy minion hordes. This is what the game currently looks like:

![](/images/towers_in_combat.PNG)

## Creating thousands of minions

To spawn the minions, we are using unit's new Data-driven technology stack (DOTS). This stack consists of multiple components, of which most are still in a preview state, meaning that they are still in development by the Unity team. DOTS constists of multiple components, the most important ones for our project being the Entity-Component-System, and the new Burst Compiler.

By utilizing those two components, we are able to write super-performant code which enables us to control and render thousands of enemy minions. However, this new technology stack also comes with new challenges. Most of the internal unity systems, like physics, rendering, and navigation, are being rewritten by the Unity team. Currently, those systems are already available to us as users of the engines, however some features are still missing or incomplete. The new systems exist alongside the existing ones.

Since some systems do not exist for the DOTS at all, we still have to use some of the classic systems, and combine those with the new systems. As a result of this, we currently have two rendering and physics systems active and in use in our project, which leads to new problems (and a lot of confusion).

Since we want to have thousands of enemy minions at a time, they present the most performance-critical part of the project. To keep the game running smoothly, we try to control the enemy minions purely using the DOTS stack, while somehow having them interact with the rest of the game, like the player's defenses for example.

## Minion Navigation

The navigation system of the DOTS is sadly still in an early stage. We can do pathfinding for each minion individually without a huge performance loss, but the DOTS solution does not allow local avoidance of the minions yet. To still enable this in our project, we wrote our orw, primitive local avoidance. This is not as good as as any of the other solutions that are on the market right now, but it is "good enough" for out case, and it works with DOTS. Sometimes it still produces some weird results:

![](/images/ezgif.com-crop (2).gif)

But since there's so many minions, the player will barely notice it if there are 2 minions too close to each other.

## New Minion Visuals

The minions are currently being spawned by 3 portals, and once they're spawned into the world they will move towards a predefined position in the world. We also updated the model of the Skeleton, since we do not plan on having any real mesh animations on the minions, which the model was initially made for. We removed the legs, made the bottom of the torso bigger, and updated the texture to make it fade towards the bottom. We also added a glow to the eyes, and made the whole model a bit "bulkier" to make the map not look that empty. To make them look alive, we are modifying their Z-Position using a sin-wave, so they really look like they're floating. The result can be seen here:

![](/images/ezgif.com-crop (1).gif)

We also added new models for the portals, added a "portal"-effect to the middle of them, and a bit of fog around it. This really helps to make the portals feel more "mysterious". We are pretty satisfied with the results:

![](/images/portals_initial.PNG)

@Timo hier kommt dein content hin (bezüglich den towern und so)

## Next steps:

The minions currently can already be targeted by the player's defenses, but they don't take any damage yet. Also, once they reach their target, they'll just disappear, instead of taking health points from the players main base. So in the upcoming week we will work on integrating the minions better with the defenses of the player.

Also, the Map currently is definitly too big, and most parts of it are currently empty. We will make the map smaller, and also update some of the assets and visuals to make it feel more alive, instead of just having all those units on a mostly empty plane.