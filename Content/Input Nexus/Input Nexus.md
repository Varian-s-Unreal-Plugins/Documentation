---
publish: true
---
InputNexus is a plugin that streamlines how Enhanced Input System is handled and where gameplay logic is stored.

- **Input Nexus Component** — Manages input actions and their Input Links.
- **Input Link** — Objects connected to input action events to execute gameplay code.
- **Link Bundle** — Enables rapid deployment of identical mapping contexts and input actions across multiple components.
- **Input Buffering** — Allows delayed execution of InputLink code through buffer channels.

The vast majority of gameplay logic around Enhanced Input System can be found in the player controller and pawn, which slowly leads to those classes becoming massively bloated. The `AC_InputNexus` actor component is designed to host your input actions and their associated `InputLinks`, which then trigger the appropriate events.

[[2026-03-31 19-29-37.png]]

## FAQ

**Should the regular `InputAction` nodes continue to be used?**

> You can, but it is advised to use `InputLinks` whenever possible because we can control the order and input consumption. This system does not block the regular input action nodes from being used in any way. The helper library comes with a `RegisterObjectWithInputComponent` and `UnregisterObjectWithInputComponent` function, which enable and disable the traditional input action nodes in most classes.

**Is it possible to have multiple Nexus components at the same time?**

> Yes! You can also enable/disable input events per Nexus component. Meaning you can disable one, then enable another Nexus component to completely swap out `InputActions` and `InputLinks`.

**For things like GAS, why wouldn't I use the in-built EIS support?**

> Every single system in Unreal that tries to tie some event to input actions are separated. So it becomes extremely difficult to debug, organize, customize and control. Lyra has its own implementation, GAS has its own implementation. `InputNexus` is a centralized system that tries to allow itself to be connected to anything you want to enable EIS support for, such as a custom ability system.

**Does this support replication?**

> No. But it doesn't mean it can't be implemented. It is fairly simple to add replication support, but it won't be added because it would mean having to provide technical support for multiplayer issues.
