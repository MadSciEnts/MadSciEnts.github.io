---
title: Ai - Generating Games
author: <SW>
categories: [Ai]
tags: [Android]
media_subpath: /media/
---

# Ai - Generating Games

This is a small investigation into the use of AI and Android development.

## Tone Generator

I was recently going to make a small tone generator in Unity.  But I came up against an issue where Unity is fundamentally unable to keep running in the background.
Thus, I turned to Android Studio to attempt a more custom solution.

After a bit of back and forth, I turned to Google's Gemini integration.

<img width="457" height="877" alt="image" src="https://github.com/user-attachments/assets/d0af8aa8-e21b-4f2e-be16-8fbd74bd0916" />

I asked it to make a tone generator for me. Along with some rough ui.

The result was fast, but not without issue.  There were frequent build errors.  But Gemini was able to resolve those iteself!

![ToneGenerator](https://github.com/user-attachments/assets/356df5fc-07f4-4349-8a8a-7e1d8031b693)


I asked it to create a tone generator that would allow for a range of 500-20,000 hz.  It had to run in the background when needed, incorporate light/dark themes. And save the last used settings.


Feel free to try it yourself.

[Download the file here](https://github.com/MadSciEnts/MadSciEnts.github.io/raw/refs/heads/main/media/apk/GDDW_003.apk)


## Simple Game

What about something more complex?


I asked Gemini to create a simple dungeon crawler with basic graphics.

![DungeonCrawler_01](https://github.com/user-attachments/assets/f35e3f4e-f857-4737-ac0e-8fa60e803d4c)


It was able to block and attack.  Simple enough.  Except when trying to grow it into something more involved.

Getting it to understand the concept of text and numbers as textures was a unique experience.  Gemini wanted to hard code the texture generation, letter by letter, pixel by pixel.
If you ask it to increase the resolution, it would.  But not in the way you would expect.

Asking for a "Game Over" screen with higher resolution text resulted in Gemini simple taking it's 8x8 texture and scaling it up.

<img width="352" height="779" alt="image" src="https://github.com/user-attachments/assets/b1f48fc2-b12f-473a-b081-c15d5406c927" />

The text wasn't exactly legible.

Being specific with prompts and assuming the unassumable is key.


After some explicit direction, I was able to get some basic legible text and simple game over screen.

![DungeonCrawler_02](https://github.com/user-attachments/assets/c5edc7e6-5930-4aef-a937-296cb9eb158a)



## Asteroids

Slowly introducing changes seemed like an excellent way to go.
Using Gemini in Android studio I asked for a simple "Top Down" space game with conservation of momentum and auto targeting of enemies.  A basic star field with parallax.

![ShipShip_01](https://github.com/user-attachments/assets/511c781e-59d9-466a-b607-e6a3f1de6aba)

It didn't do a terrible job!  Text was still a hurdle.  Support for landscape vs portrait orientation was an issue as well.  It created multiple layouts and configurations for each need.
Adding lots of complexity in areas according to the directions it was given.

Other issues arose such as weapon projectile collision vs ray cast for accuracy.

![ShipShip_02](https://github.com/user-attachments/assets/9d4fa649-d045-45d9-8d55-513023ef36b9)

In the end, Gemini painted itself into an recoverable corner and the project was in an unbuildable state.

Because I had such a long conversational history of revisions and requests, the context the AI had to parse through resulted in frequent Request Timeout's.

Eventually, the AI just kept repeating the same changes to the same files over and over and over again.


## Ai as the Middleman?

It became aparent that 'evolving' the generation of a mobile game by slowly increasing complexity wasn't the right way to go about it.  A series of relatively simple prompts quickly run awry with unrealized assumptions. Both from the Ai and the User.


But what about using Ai to create a better framework?

Android Studio used Gemini integration.  But what if I used other Ai to describe the framework in a cleaner more approachable way?


I posed the same question to several Ai Agents.  Gemini, ChatGPT, and Grok.

This was my prompt to each of them:

```
Choose a well known and effective framework for creating simple mobile video games.
Similar to a simple action RPG.
Describe the framework in detail in such a way that it could be used as a guide for creating a mobile game.

The framework should support a "Top Down" 2.5d game where the player controls a spaceship that has inventory
and weapon ports.  The player ship should "evolve" in complexity to support increasing size and number of weapons.
The weapons should be broken up into 3 categories: Projectiles, Beams, Missiles.
The player and enemy classes should inherit from a common base class.  On screen controls should be used.
On Screen Joystick for motion. On Screen buttons for attack and manipulation of inventory.
Spaceships should not have initial motion, but maintain momentum with little or no drag.
Background should be of a particle based starfield that shows parallax.  Color variation should be a prevalent
theme denoting importance or rarity of object.  Starfield should have 40% color and intensity variation.
Player HUD should have progress bars for any attributes like health and shield prominently displayed.
An experience counter / bar should be used/shown to indicate when player is going to level up and evolve.
Textures should be procedurally generated for all HUD elements, weapons, and effects using a pixelated style.
Any text should be of a 64x64 character resolution for legibility.


Describe this framework as an effective prompt for the creation of a mobile game in Android Studio using Gemini ready to play. 
```


### Results

#### Gemini

Oddly enough, the prompt Gemini gave involved LibGDX and some libraries that weren't compatible with eachother.  The end result was an infinite loop of build fixes.  



#### ChatGPT

ChatGPT returned a detailed prompt of how to approach the project in Godot and Unity instead.  It offered to start generating some of the physics modules to get started.  



#### Grok

Grok also suggested LibGDX.  But it gave a more structured prompt to feed Gemini within Android Studio.

Surprisingly the result was basically playable!

I asked it for some alterations.
- Radar System
- Infinite levelling (add weapon slot every 5 levels of experience)
- A 'charge weapon' feature (depleating shields for the sake of a intense blast)
- Debug weapons to jump through experience levels (on the side of the scren).
- Ships that grew in size according to experience level.


![ShipShip_03](https://github.com/user-attachments/assets/619c6105-e1b7-4797-a4ee-2084add2a579)


The result was basically playable.  It still had issues regarding a background star field.

[GitHub Docs](https://github.com/MadSciEnts/ShipShip "ShipShip Repo")


Try it for yourself.

[Download the file here](https://github.com/MadSciEnts/MadSciEnts.github.io/raw/refs/heads/main/media/apk/GDDW_007.apk)
