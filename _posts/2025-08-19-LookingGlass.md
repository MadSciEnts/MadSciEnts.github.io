---
title: Looking Glass
author: <SW>
categories: [holography]
tags: [experiment]
media_subpath: /media/LookingGlass/
---

For many years, I've been fascinated by 'magic eye' posters and 3d movies. 

The only problem is the strain it puts on our eyes. Often leading to headaches. This is part of the reason 3d movies and TV have fallen out of style. 

What if you didn't need special glasses? Would that make the experience any better? 

Believe it or not, the technology exists at the consumer level. 

One such product is 'Light Field Displays' by a company called 'Looking Glass'.


Looking Glass Light Field Displays are type of naked eye holographic display.
<https://lookingglassfactory.com/>
It is advertised for use in the fields of medicine and engineering.


The basic idea is the same as those cards they had many years ago. The ones that you could tilt and see different images. This was possible due to the clear plastic cover with grooves in it. The grooves split the view of the image so you should only see one part at a time. 


Looking Glass displays work in a similar way. With more complicated grooves.


Stereographic 3d movies and films utilize 2 images.
One for the left eye, and one for the right eye.

![Desktop View](/cube_single.png){: w="70" h="95" } ![Desktop View](/cube_singleR.png){: w="70" h="95" }
>These images are reversed.
>You can cross your eyes to see the 3d image.
{: .prompt-tip }

Naked eye holographic displays are a bit more involved.
Instead of just 2 images for right and left, they use 48 images. The result is a range of angles from left to right. 

We render these 48 images into a grid and store them as a single large image read by the display.

![Desktop View](/test_cube.PNG){: w="256" h="256" }

This is so that no matter the angle you view the display from each eye will perceive a different image. Giving you the illusion of depth.

However 3d displays have a limited range of depth. This is often determined by the size of the screen. But almost always proportional.

For example, 3d movies in the theatre can give the illusion of several feet in front of the screen, and many feet deep behind the screen. Smaller displays like the one I was exploring have a limit of a few inches infront, and a few inches deep behind the screen. If you try to exceed these limits it will result in great eye strain and headaches.


One way we can push this illusion even further while remaining within display limitations is to introduce reflective surfaces in our renders.

![Desktop View](/room_single.png){: w="256" h="256" }

In the above example we have a simple room. 

In this room is a mirror. I was curious if this mirror would add to the sense of depth. 

The display itself seems to support a relatively shallow physical depth. Roughly 1-2 inches in front and 2-4 inches behind. 

With reflective surfaces it might be possible to give the illusion of more space to the sides than we actually see in the frame.


![Desktop View](/room.png){: w="256" h="256" }

In the above image you can see the 48 images that were rendered. If you look closely, the reflection in the mirror shows a good deal of different perspectives through it. 


The result, when viewed through the display, is a real sense of depth.

![Desktop View](/room.gif){: w="256" h="256" }



Of course, there are limits to just how much depth you can reliably perceive.

Just like in 3d movies, there is an optimal range for perception that the technology will support.

Reflective surfaces help us to push past the limits of the display. 


To push these tests a little bit further, I tried using an example scene with boats and sails.


![Desktop View](/ocean_single.png){: w="256" h="256" }


There are 3 main concepts in any 3d image regardless of display. 

The point closest to the audience is the 'near clip'. This is where a virtual camera starts to 'see'.

The point in space with no depth is the 'focal point'. The pixels at this depth won't change from angle to angle, or image to image. 

The farthest point is the 'far clip'. This is the farthest point a 3d camera can see. In 3d movies, it's also known as the 'infinity plane'.

Because the Looking Glass display can only give the illusion 1-2 inches in front of the focal plane and 2-4 inches behind, I was curious how close to those limits could be viewed comfortably.


The top of the sails are a nice crisp point close to the viewer. Perfect for a near clip point that won't strain the eyes. 

The ocean surface itself with ripples and wake is perfect to sit on the focal plane. 

Finally, the ocean depths are foggy and excellent to give the illusion of extreme depth without adding eye strain.


And the final result is below.

![Desktop View](/ocean.gif){: w="256" h="256" }

This is the full 48 frames feed into the display. 

![Desktop View](/ocean.png){: w="256" h="256" }




This technology has a lot of promise for medical or architectural displays.


But I also feel it would be great for product kiosks or advertisements. Jewelry kiosks could also benefit, without risking theft.



Going to the opposite extreme, I was curious if fur with fine detail would also display well.

Fur isn't shiny. Would it give a decent sense of depth if it has enough range of depth in space?

Sadly, the answer appears to be 'no'.
The fine detail in the fur isn't captured accurately, due to limitations in resolution. The overall general shape of the fur clumps are presented well enough. But still to soft overall.

![Desktop View](/fur.gif){: w="256" h="256" }



Conclusion: 

While naked eye holographic displays are still in their infancy.  Where they really shine... is shiny and translucent surfaces, with as many depth cues as possible.  Very similar to 3d movies.  I firmly believe they have missed their calling in advertising or kiosk displays.
