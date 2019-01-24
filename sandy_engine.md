---
layout: default
title: Sandy Engine 
permalink: /sandy-engine/
published: true
---

## About

{: style="text-align: justify;"}
Sandy Engine is procedural terrain generator created for Planet Nomads game [Planet Nomads](https://www.planet-nomads.com) 
written in C++11 and used as plugin for the Unity Engine. It provides generation of spherical terrain surface, water 
surface, procedural cave system, object and grass placement. Whole planet surface is consist of biomes describing how
the environment look like and how it interact with player. For the biome placement and biome creation we designed
various set of editors and custom tools for designers. 

#### Biome distribution on the planet:

{: style="text-align: center;"}
![biomes]({{ "/pics/biomes.jpg" | absolute_url }})

{: style="text-align: justify;"}
Round planet surface is generated in realtime when the player travel around, so speed was one of the most important things here. 
The terrain is divided into chunks with different sizes of voxels depending on distance from the player. Terrain geometry
closer to the player has more details.

#### Final terrain in the game 

{: style="text-align: center;"}
![biomes]({{ "/pics/terrain.jpg" | absolute_url }})

Source code of this project is not available.

## Used techniques
- **Marching Cubes** for mesh creation. [Wiki](https://en.wikipedia.org/wiki/Marching_cubes)
- **Octree** for fast surface search and chunk management.
- **Noises** for procedural generation (perlin, voronoi, ridged-multi, ...)
- **Multithreading** for faster terrain generation.
- **SQLite** database for storing player-created modifications of the terrain.
- **Custom memory management** for faster memory allocations. 

## Links

[Planet Nomads official page](https://www.planet-nomads.com)

[Planet Nomads on Steam](http://store.steampowered.com/app/504050/Planet_Nomads/)
