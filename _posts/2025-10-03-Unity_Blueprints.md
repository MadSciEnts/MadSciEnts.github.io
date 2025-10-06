---
title: Unity - Blueprint System 
author: <SW>
categories: [Unity]
tags: [Experiment, VR, Blueprints, NodeGraph]
media_subpath: /media/unity/
---

# Unity Blueprint Tests

![Graph Editor](kraken_graph_editor_03.PNG)

There are a lot of issues that arise when creating VR content in Unity3d.
I was curious if some of these could be resolved with a custom toolset to allow for rapid development with a small team.

In that persuit, I created 'Kraken'.  A multi pronged procedural node graph system to generate games and levels.  A basic GUI could be dynamically generated.  Initial level designs based on game type, setup and ready to go. 


Want a 2d side scroller? Add a side scroller game node to the scene graph.  VR co-op?  Swap the 2d game node for a VR game node.  Each node would contribute to the game architecture.  Nodes could add assets to a scene. Node connections would connect scene objects. Nodes to establish scene hierarchies.  And establish game loops and logic.


## Philosophy of Node Graphs

Nodes were broken up into several categorical concepts.  But they all had to interact together. 


1- Asset nodes would load an asset and make it available to other nodes in the graph. 


2- Hierarchical nodes would handle parenting, layout transformation, and instancing.


3- Logical nodes would manipulate game logic or general processing of scene assets as provided by asset nodes.


The tricky part was ensuring it could work in reverse.  Capture an existing open scene, and transpose it to scene graph representations.  Primarily for recording scene layout as node representations for future reproduction at run time.


## Starting Point


It was derived from a node editor framework (https://github.com/Baste-RainGames/Node_Editor) which allowed for extending it to serve my needs.

These node graphs were meant to be designed in the editor and processed at runtime.

I added an asset management system that supported tagging and basic version control. Even if a level were designed with out of date assets, when the level was loaded it would utilize the latest published in the asset library.
Kraken also supported 'hot swapping' asset library locations at any time. this allowed for different asset 'collections' to be operated upon.  In this sense 'asset libraries' were very much like asset 'themes' as well.


## Kraken


![Graph Editor](kraken_graph_editor_03.PNG)

[Kraken Blueprint System for Unity3D 2017](https://www.youtube.com/watch?v=uZdvtt_UBb8)

Here is a quick video of the Kraken node based system dynamically restoring deleted or destroyed parts of the level scene hierarchy, based on the nodes in the graph.
If the nodes had all of their 'required' input conditions met, the connections would light up in the color of their asset type.
Cameras would connect to UI Panels. Ui Panels would connect to UI Managers to handle transitions, and so on.


## General Theory


The scene graph would be saved as a scriptable asset, loaded to a null transform within the scene as an 'anchor'.  The graph editor would look to find any graphs attached to the scene and allow you to view the graph and exectute it as requested.  Several versions or 'layers' could be saved on a single transform anchor node in a scene.  This would allow you to quickly iterate between scene graphs before comitting a graph for export as a versionable asset.  As many scene graph achors could be located in a scene as you need.  One achor scene graph for ui, one for layout, one for lighting, etc.  I also found it useful for layout prefab generation. Using a scene as a prefab 'factory' of sorts to generate versions of rooms or locations.  While also allowing quick iteration or hot swapping of sub prefab assets (like floor tiles, columns, lights, etc) to visually determine the best modular part to use in a larger whole.


## Kraken Repo


If you'd like to try it out yourself, this is a git repo of an early vanilla Kraken.
It requires [Unity3d 2017](https://unity.com/releases/editor/archive)

[Kraken 2017 Unity3d Repo (*REQUIRES UNITY 2017*)](https://bitbucket.org/logicsquid/kraken_2017/src/main/)


## Limited Success


Here and there, I tried to keep improving the toolset to support VR and other advancements.  VR integrations substantially evolved into what is now called XR.  My goal was to be able to rapidly prototype a multiplayer coop videogame that supported crossplay between Mobile, Console, PC, and VR(XR).  With full controller support.  Unfortunately (as with all things) work and 'life' got in the way.  

Along the way I attempted many experiments.  Dynamic level destruction, enemy armour destruction, goal based ai, etc.  All the while keeping an eye on optimization and ensuring frame rates were over 90fps.

While no longer supported, Kraken was able to allow me to prototype an idea within a day or two.  In that regard I consider it a limited success.

Media Links:

[Procedural Layout Tool - Swapping Lights](https://www.youtube.com/watch?v=NDlg-uK0NFI)


[Procedural Layout Tool - Swapping Prefabs](https://www.youtube.com/watch?v=_c9elP4yZAk)


[VR Enemy Test](https://www.youtube.com/watch?v=_Hr0AfRI6nk)


[VR Destruction Test](https://www.youtube.com/watch?v=SsS8OVXHfko)



# Git Repositories of other tests

Early VR Prefab assets for Unity
[LS_VR_PREFABS](https://bitbucket.org/logicsquid/ls_vr_prefabs/src/master/)

Misc VR Scripts and Utils
[LS_VR_SCRIPTS](https://bitbucket.org/logicsquid/ls_vr_scripts/src/master/)

Procedural Dungeon tools and scripts
[LS_DSCRIPTS](https://bitbucket.org/logicsquid/ls_dscripts/src/master/)

LogicSquid Early Toolset
[LS_TS](https://bitbucket.org/logicsquid/ls_ts/src/main/)

Steam VR Early Overrides
[SteamVR](https://bitbucket.org/logicsquid/steamvr/src/master/)



# Other Early Android Prototypes

## Escape Pawn

[Escape Pawn](https://youtu.be/5sR0MXlD1n8)

Early experimentation with noise based level destruction.  Circa Unity3D v3.5


## The Shootening

[The Shootening](https://www.youtube.com/watch?v=MPRKRf6xgtw)

Early particle stress testing on Android device. Target was to keep draw calls under 12.
