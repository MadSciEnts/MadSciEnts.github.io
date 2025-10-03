---
title: Making Waves
author: <SW>
categories: [unity,tessendorf]
tags: [water]
media_subpath: /media/
---

# Explorations into Unity and wave simulations.
![Desktop View](/tessendorf_waves_v001.gif){: w="512" h="262" }

Wave simulations in games are always tricky.
>It's real time and needs to be efficient.
{: .prompt-tip }

My goal was two fold.

1. Get fun looking water, on modest mobile devices.
2. VR. Can it run fast enough to maintain a high frame rate in VR?



I was first aware of Tessendorf water algorithms while working at MPC on a movie called "The Finest Hours".


On that project, the water needed to have character, motivation, and tell a story.


That meant we had to make water sims something that animators could control, and later drive simulated water iteractions in Houdini.  That's no easy task.

Fortunately, MPC had some top minds exploring the concept.


We ended up using tessendorf water within Maya as an animatable asset. Fully rigged geo plane with animatable controlers.  Where animators could control the amplitude, freq and many other parameters to get realtime playback within the viewport.


But what about Unity3d?


Once again, smarter minds had already explored the concept!

Unfortunately, this was well over a decade ago, and the experimental Unity Tessendorf I was able to find, no longer exists.


But I did find this amazing post which presents an even more efficient solution!

>Please check out his GIT repo containing a Unity project. <https://antoniospg.github.io/UnityOcean/OceanSimulation.html>
{: .prompt-tip }

This was basically my starting point.  What I was trying to explore was not impossible.



With enough tweaking, and some HLSL shaders I was able to code from scratch, I was able to get some very promising results.

Nowadays, Unity has a rhobust node based shader pipeline.
Back in the day, this was not the case.  Even less so for Mobile deploys.

With some creative shortcuts and optimization, I was able to get some infinite water actually working in VR!

It was quite amazing. Sitting on a virtual boat and travelling a virtual ocean is one of my earliest VR experiences that I will never forget.

Unfortunately, it was some time ago.  But I did find an old screen capture of my final shading result.

![Desktop View](/tessendorf_waves_v001.gif){: w="512" h="262" }

I was quite proud of the result with high res textures and quality reflection maps.


Some time later, I was exploring the idea of stylized water.

Once again, Tessendorf to the rescue!

I pre rendered a spherical reflection map.

Then, tweaked the shader code for optimization and fewer texture maps.
Increased the polygon density.

And Voila!!
![Desktop View](/tessendorf_stylized_v001.gif){: w="488" h="374" }

This was a screen capture from within VR.
While it didn't quite achieve the brush stroke stylized effect I was going for, I still enjoy the result.
