# Lab for Week 4, Session 1 - Animations in Unity

This lab focuses on Unity [animations](https://docs.unity3d.com/Manual/AnimationSection.html).

## Overview

You can animate _GameObjects_ in Unity using traditional [keyframe](https://en.wikipedia.org/wiki/Key_frame) animation techniques. Keyframes are points on a timeline that contain data about a _GameObject's_ position, or scale. Essentially _keyframes_ indicate a change that produces an animation, so that, when it plays, Unity is able to interpolate the data from one keyframe to the next, thus animating the object.

## Make a Plant Grow

Below, you are going to make a flower grow. This is a special flower that only blooms for you - it will only grow when you are near and when you tell it to. And when you leave, it whithers away.

### The Animation

Open [Unity Hub](https://docs.unity3d.com/Manual/GettingStartedUnityHub.html), and open the project from the last lab.

First, you will need another asset, so go to the [Unity asset store](https://assetstore.unity.com/) and import [Lowpoly Flowers](https://assetstore.unity.com/packages/3d/vegetation/plants/lowpoly-flowers-47083).  Before you can use the imported assets, ensure they can use the High Definition Render Pipeline; so go to _Edit_, _Rendering_, _Materials_, _Upgrade HDRP Materials..._ and _Convert All Built-in Materials..._.

Create an empty _GameObject_, and name it _Flower_, then drag one of the _Lowpoly Flowers_ into that. This step means that any animation you create on the _Lowpoly Flower_ will be animated relative to the position of the _Flower GameObject_ and not the scene itself. Position the _Lowpoly Flower_ so that it is front of the door, then scale it so it is 10 across all three axis, as it is in Figure 1, below.

![](./images/flower.png)

_Figure 1: The Flower_

Now we're going to animate the flower using two animations - one for when it is hibernating, waiting for you to come nearby, and the other for when you tell it to grow.

First, create an _Animations_ folder in the _Project_ tab. Next, go to _Window_, _Animation_, and dock the tab wheresoever you wish. Select the _Lowpoly Flower_ in the _Hierarchy_ and click on _Create_ in the _Animation_ window. Select the _Animations_ folder you created above and call the animation _Hibernation_. With the animation timeline at 0, press _Record_, then move the flower so it is below ground. Stop recording. Move the animation timeline forward half-a-second and press _Record_ once more. Move the flower's position ever-so-slightly, but ensure it remains below ground. Stop recording. Now _Create New Clip_, call it _Flourish_, and with the animation timeline at 0, press _Record_. Again move the flower so it is below ground and Stop recording. Move the animation timeline forward two seconds and press _Record_ once more. This time, move the flower's postion so it is above ground. Stop recording.

Find the _Flourish_ animation in the _Project_ tab, and in the _Inspector_ tab, unset _Loop Time_ - you want the flower to stay in bloom until you leave.

Select the _Lowpoly Flower_ in the _Hierarchy_, and from the _Inspector_ tab, open up the _Animator Controller_. In the controller's _Parameters_, add two Triggers, "Grow" and "Hibernate". Now add a transition from _Hibernation_ to _Flourish_, and visa-versa. Highlight the transition from _Hibernation_ to _Flourish_ and add the "Grow" _condition_. Highlight the transition from _Flourish_ to _Hibernation_ and add the "Hibernate" _condition_. Figure 2 shows what your _Animator Controller_ should look like.

![](./images/animationController.png)

_Figure 2: Animation controller_

Finally, you need a script to make the flower bloom and hibernate, so create a _C# Script_ called _Grower_, and make it look like this:

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Grower : MonoBehaviour
{
    [SerializeField] private string playerTag;
    [SerializeField] private string hibernateTrigger;
    [SerializeField] private string growTrigger;

    private Animator animator;
    private bool inTrigger = false;

    // Start is called before the first frame update
    void Start()
    {
        animator = GetComponentInChildren<Animator>();
    }

    // Update is called once per frame
    void Update()
    {
        if((Input.GetKeyDown(KeyCode.G)) && inTrigger )
        {
            animator.SetTrigger(growTrigger);
        }
    }

    private void OnTriggerEnter(Collider other)
    {
        //Debug.Log("In here");
        if(other.tag == playerTag)
        {
            inTrigger = true;
        }
    }

    private void OnTriggerExit(Collider other)
    {
        //Debug.Log("Exiting here");
        if (other.tag == playerTag)
        {
            inTrigger = false;
            animator.SetTrigger(hibernateTrigger);
        }
    }
}
```

Drag the _Grower_ script onto the _Lowpoly Flower_ in the hierarchy and set its _Player_ field to "Player", the _Hibernate_ field to "Hibernate" and the _Grow_ field to "Grow" in the _Inspector_. Ensure your _PlayerCapsule_ (FPSController) has the "Player" tag set. Finally, add a _Box Collider_ to the _Lowpoly Flower_, set _Is Trigger_ and position and size the collider so it looks similar to Figure 3, below.

![](./images/boxCollider.png)

_Figure 3: Box collider_

When you press _Play_, you _may_ get the error, _InvalidOperationException: You are trying to read Input using the UnityEngine.Input class, but you have switched active Input handling to Input System package in Player Settings._ That is because you switched to Unity's new _Input System_ in a previous lab, yet, in the script above, you're using the legacy input system when calling `Input.GetKeyDown`. The simplest way to fix that in this instance is to go to _Edit_, _Project Settings_, _Player_ and switch _Active Input Handling_ to _Both_.

_Play_ should work properly now, so when you walk near the flower and press _G_ on your keypad, your flower will grow and bloom, as in Figure 4. And when you walk away, it will wither away, inconsolable because you've left.

![](./images/flowerInBloom.png)

_Figure 4: Flower in bloom_

You can play around with the timings of the transitions to make the flower grow and wither at different speeds. Those are left as exercises.

## Extended

The way I crafted the animations to make the flower hibernate and grow is not the only way I could have done it - can you find other ways?

Animate other game objects in the scene - for example, you could put an actual door onto the front of the container, which you animate so it opens and closes.

Similar to previous labs, if you have experience with [Blender](https://www.blender.org/) or [Cinema4d](https://www.maxon.net/en/cinema-4d), try importing and using an animation from them.

## Useful Links

+ [Animations](https://docs.unity3d.com/Manual/AnimationSection.html)
+ [Animator Controller](https://docs.unity3d.com/Manual/class-AnimatorController.html)
+ [How to Animate in Unity 3D](https://www.youtube.com/watch?v=sgHicuJAu3g)
