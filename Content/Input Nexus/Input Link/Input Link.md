---
topic: "[[Input Nexus]]"
publish: true
priority: "2"
---
# Input Link
When it comes to running meaningful gameplay code, `InputLinks` is where that code is stored.

Links are tied to an `InputAction` and `TriggerEvents` to control when their code is ran. When that action is activated with that trigger event, the `InputLink` will call `OnInputActivated`

Input events are handled like so:

![[Pasted image 20260331194119.png]]

* Links can be dynamically enabled and disabled, for example an ability input being disabled while the ability is on cooldown.
* Links will only receive the input event if:
  * They are registered to the specific trigger event that is currently occurring.
  * `CanHandleInput`returns true&#x20;
  * The link is enabled.
* If the link decides to consume the input, it will prevent the input event from continuing on down the chain of links for that input action.
* To add a input link during runtime, in Blueprints use the `ConstructObjectFromClass` node, this will allow you to edit `ExposeOnSpawn` parameters as you wish. In C++, use `NewObject<>()`. Then call `AddInputLink`.

***

## Runtime Input Links
`InputLink`'s can be constructed during runtime. Sometimes, all you need is to listen to an input event as if the object is an input link. For example; a GAS ability

![[Pasted image 20260331194231.png]]

This GAS ability is now receiving input events as if itself was an `InputLink`. The events are just being filtered and forwarded through a `InputLink`, making it act as a proxy between `GAS` and `InputNexus`.

This method now allows you to utilize all the strenghts of `InputNexus` with minimal work and complexity. This ability can now benefit from input buffering, input consumption and more.

***

## Practical examples
* During the tutorial, you might want to listen to specific input events, such as the movement keys. Normally, you'd now have to hard code this into the player character and have redundant code throughout your entire game. With a `InputLink`, you can listen to an input event, execute custom code, then remove it. Separating that logic from the character and not have redundant code being executed throughout the game.
  I use the FlowGraph plugin to add a input link to the jump and movement input actions during the tutorial and broadcast an event when it happens. The input link has then been designed to remove itself when it hits a broadcast limit.

![[Pasted image 20260331194240.png]]

![[Pasted image 20260331194247.png]]

* For my project, I've integrated support with [**ObjectTags**](https://app.gitbook.com/o/tef4Pdm43BXhZOKh9XrE/s/jP5XAKMs1xUM2psZ0ZK9/) so I can natively block `InputLink`'s depending on a tag query. Now all I need to do to block movement is fill in what tags would block the movement `InputLink`, such as a stunned tag. I never have to repeat this code anywhere, I just need to make my `InputLink`'s a child of this tag support class.

![[Pasted image 20260331194258.png]]

***

## Creating custom input links

`InputLink`'s have several functions for you to override and call.

![[Pasted image 20260331194309.png]]

> [!INFO] Title
> `InputNexus` comes with 2 simple examples, which can be found in the `Links` folder.


The majority of the time, you'll be overriding either `OnInputActivated` or `CanHandleInput`

# See also:
- [[Nexus Component]] - The host for input links.