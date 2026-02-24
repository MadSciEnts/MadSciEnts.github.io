---
title: Ai - Generating Games
author: <SW>
categories: [Ai]
tags: [Android]
media_subpath: /media/
---

# Ai - Generating Games

This is a small investigation into the use of AI and Android development.


I was recently going to make a small tone generator in Unity.  But I came up against an issue where Unity is fundamentally unable to keep running in the background.
Thus, I turned to Android Studio to attempt a more custom solution.

After a bit of back and forth, I turned to Google's Gemini integration.

<img width="457" height="877" alt="image" src="https://github.com/user-attachments/assets/d0af8aa8-e21b-4f2e-be16-8fbd74bd0916" />

I asked it to make a tone generator for me. Along with some rough ui.

The result was fast, but not without issue.  There were frequent build errors.  But Gemini was able to resolve those iteself!

![ToneGenerator](https://github.com/user-attachments/assets/356df5fc-07f4-4349-8a8a-7e1d8031b693)


I asked it to create a tone generator that would allow for a range of 500-20,000 hz.  It had to run in the background when needed, incorporate light/dark themes. And save the last used settings.


Feel free to try it yourself.

[Download the file here](https://github.com/MadSciEnts//user/repository/branch/filename)
