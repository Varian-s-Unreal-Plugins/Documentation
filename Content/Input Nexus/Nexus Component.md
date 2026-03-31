---
topic: "[[Input Nexus]]"
publish: true
---
# Nexus Component

This component is the host of all `InputLink`'s and manages them. It's also responsible for link bundles, mapping contexts and buffering inputs.

## Buffering inputs

To open and close an input buffer channel, simply call `OpenInputBufferChannel` and `CloseInputBufferChannel`. Go [here](https://varian.gitbook.io/varian-docs/input-nexus/input-link/input-buffer) to read more about how input buffers work.

* You can check if a channel is open through the `IsBufferChannelOpen` function.

## Managing inputs

* To completely disable or enable a `NexusComponent`, call `ToggleInputEvents`. You can also call the native `Activate` or `Deactivate` functions, which will toggle the input events appropriately.
* To disable or enable an input action, call `ToggleInputEventsForInputAction`.
* Multiple `NexusComponent`'s are supported on an actor, but it's up to you to retrieve the one you want. You might want to create a list of what type of input logic the pawn will use and what kind of input logic the controller will use.\
  For example:
  * Controller: Handles UI logic, such as the escape button summoning the escape screen.
  * Pawn: Handles movement and interaction. In the case that the player possesses a vehicle pawn, this will automatically disable the other pawns movement and interaction events.

# See also
- [[Input Link]] - The host of gameplay logic.