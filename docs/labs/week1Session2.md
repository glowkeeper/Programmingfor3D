# Lab for Week 1, Session 2 - Graphics in Unity - Lighting

This lab introduces you to graphics and lighting in [Unity](https://unity.com/).

## Overview

Unity comes with a range of lighting techniques whose aim is to approximate the reality of light's behaviour. The result is that Unity can generate photo-realistic graphics, or, as in Figure 1, something much more stylised.

![](./images/fe.png)

_Figure 1: [Fe](https://www.ea.com/games/fe)_

Unity models direct and indirect light - to get realistic effects, you must combine both. Direct light is emitted from a source, hits a surface, and gets reflected directly into a sensor (such as a virtual camera). Indirect light is all other light; it includes ambient environmental light that comes from the sky that may have been reflected many times from different surfaces before it reaches a sensor (for more technical information on this subject, please see [3D Graphics](../graphicsBackground.md). **And do remember, for your assessment for this module, you will almost certainly have to write about some of the material in that document**. Best to learn it now!).

Unity uses a global illumination (GI) system that is currently supported by two separate systems, 1) Realtime GI and 2) Baked GI. Realtime lighting is calculated at runtime. Baked lighting is light data that is computed in advance and gets _applied_ at runtime (rather than calculated). Ultimately, the difference is a trade-off between runtime performance (realtime lighting) and the time it takes to render your 3D graphics beforehand (baked lighting).

## Lighting a Simple Scene

Below, you will create a simple scene that introduces some of the lighting capabilities of Unity.

### A Simple Room

Open Unity Hub, create a new project and choose the 3D Sample Scene (URP) - this is a scene that uses the Universal Render Pipeline (URP) template. Name the project however you choose.

The loaded URP sample scene is an opportunity to play with Unity's lighting systems. Figure 2 shows the rotational tool being used to change the direction of lighting. When you do the same, notice how it affects the workshop's shadows.

![](./images/sampleScene.png)

_Figure 2: Lighting the sample scene_

However, you are not going to use the sample scene; instead, you are going to create your own, so click on _File_, _New Scene_ and select _Basic (Built-in)_. You are going to model a room with no windows, so first set up the project to support that. Go to _Window_, _Rendering_, _Lighting_, _Environment_ and set _Skybox Material_ to _None_. On the _Scene_ tab in _Window_, _Rendering_, _Lighting_, click on _New Lighting Settings_ and ensure _Baked Global Illumination_ is selected. Set _Lighting Mode_ to _Baked Indirect_, turn on _Ambient Occlusion_ and turn on _Auto Generate_.

At this point, you may also wish to set the Main Camera's _Background Type_ to some _Solid Colour_ that makes your room stand out in the Game view. Later on in the module, you will use _Post Processing_ rendering, so take the opportunity to turn that on, too.

Now create five copies of _GameObject_, _3D Object_, _Plane_, which you should transform to model a simple room similar to that shown in Figure 3. Also, create an empty _GameObject_, move the five planes into that, rename it to _Room_ and make it _static_ so Unity can pre-compute some of the properties of your room. You may also wish to rename your five planes appropriately, too.

![](./images/simpleRoom.png)

_Figure 3: A simple room_

Now is an excellent time to save your newly created scene and project.

You are going to light up your scene. First, we're going to need a lamp asset, so go to the [unity asset store](https://assetstore.unity.com/), and add the free [PBR LAMPS PACK](https://assetstore.unity.com/packages/3d/props/interior/free-pbr-lamps-70181) to your Unity assets by downloading and importing that into your project. Before you can use the imported lamps, you must update them to use URP; so go to _Edit_, _Rendering_, _Materials_, _Convert..._. Now drag the _Large round lamp_ [prefab](https://docs.unity3d.com/Manual/Prefabs.html) into your room in the scene, and use a transform to scale it to a size of your liking. Then position it in the middle of your ceiling and ensure the lamp is facing into the room.  

Currently, the lamp does not emit any light, so you are going to change that by adding a _Point Light_; do so by going to _GameObject_, _Light_, _Point Light_. Move it until it looks as though the lamp is emitting light and play around with the settings until you find a colour and intensity that you like.

Lastly, we want to adjust the directional light. Just keep in mind that this is supposed to be an inside scene, so we do not want ambient directional light to have too much of an affect. There are a number of ways to achieve this; first, might be just to delete it; indeed, Figure 4 shows the Game tab with the _Directional Light_ deleted, and the _Point Light_ added to the lamp.

![](./images/simpleRoomLit.png)

_Figure 4: A simple room with added materials_

However, you may choose to do things differently! For instance, you could switch the directional light's _Mode_ from _Realtime_ to _Baked_, when it appears to obey the geometry much better (since there is no front wall at the moment, you may need to change some parameters to ensure the light is not affecting the room).

Save your scene and save your project. You will add to this in the next lab.

## Extended

Play around with the directional light so that the room's shadows appear to be cast by moonlight. Additionally, look at some of the _Environment Lighting_ settings for the Lighting - perhaps change the _Source_ to _Gradient_, and see the effect of changing the _Sky_, _Equator_ and _Ground_ colours.

Furthermore, instead of building your room with simple 3D objects, perhaps use [ProBuilder](https://docs.unity3d.com/Packages/com.unity.probuilder@5.0/manual/index.html), and create something more complex. You could even import a model from [Blender](https://www.blender.org/) or [Cinema4d](https://www.maxon.net/en/cinema-4d) if you have experience with those.

## Useful Links

+ [Explore the Unity Editor](https://learn.unity.com/tutorial/explore-the-unity-editor-1#)
+ [Unity Tutorials](https://learn.unity.com/tutorials)
+ [LEARN UNITY](https://www.youtube.com/watch?v=pwZpJzpE2lQ)
+ [BRACKEYS](https://www.youtube.com/user/Brackeys)
+ [SYKOOTV](https://www.youtube.com/user/SykooTV)
+ [Lighting](https://docs.unity3d.com/Manual/LightingOverview.html)
+ [Tutorial - Introduction to Lighting and Rendering](https://learn.unity.com/tutorial/introduction-to-lighting-and-rendering-2019-3)
+ [Global Illumination](https://docs.unity3d.com/560/Documentation/Manual/GIIntro.html)
+ [Light Mode - Baked](https://docs.unity3d.com/Manual/LightMode-Baked.html)
+ [Types of Light](https://docs.unity3d.com/Manual/Lighting.html)
+ [Skybox](https://docs.unity3d.com/2020.3/Documentation/Manual/skyboxes.html)
+ [Ambient Occlusion](https://docs.unity3d.com/Manual/LightingBakedAmbientOcclusion.html)
+ [Backface Culling](https://answers.unity.com/questions/1447454/mesh-looks-transperent-on-one-side.html)