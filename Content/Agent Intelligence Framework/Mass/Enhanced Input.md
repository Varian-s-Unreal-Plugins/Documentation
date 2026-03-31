`AIF` provides a very simple fragment to categories specific signals to specific input actions and forwarding those signals to an entities and their children.

The primary use case for this is for action bars, where an entity might have children entities (such as ability entities) you want to signal when a specific input action is triggered. It is then up to the signal processor to tell that entity to do the gameplay logic you want.
- Remember, `Enhanced Input` allows you to inject inputs for any controller. Meaning, if you give an NPC entity an Entity Controller, you can inject inputs for it and allow them to also participate in this system.

To use this system, you call `SendInputSignalByTag/Name`.
![[Pasted image 20260331155406.png]]

For an entity to participate in this system, they must have the `FEntityInputActionFragment` fragment, which can be granted by the `InputActionTrait` trait. This can also be granted by calling `AddInputSignalToEntity`. This function can also be used to modify the fragment.

- The input entity is not mandated to have the fragment. The input entity can be a parent who has entities who are using the fragment and they will still be signaled.

For an entity to stop participating, you can either remove the fragment or call `RemoveInputSignalFromEntity` if you just want to remove a specific signal.


## Creating input signal processors
- Create a processor subclassing either `UMassSignalProcessorBase` or `UAgentIntelligenceCoreSignalProcessor` and set it up. (subscribe to your signals, execution order, etc)
- Add `FEntityInputActionFragment` to your entity query
- Override `SignalEntities` and in your entity loop, get the input action fragment to retrieve the payload and then perform your logic
The plugin provides an example; `UActivateAbilityInputSignalProcessor`

## Notes
- The main limitation this system currently has is that there's no comfortable way of retrieving the input action data (such as the event type or action data). The Mass developers have talked about giving Signals "Payloads" which would fix this problem. Though there doesn't seem to be a timeline for this.​
    - For now, the input action fragment has a `Payload` variable. This variable is filled when an input signal is sent.
- It's recommended to use the tags version as often as possible, since blueprint `FName`'s require you to manually type in the text, which can lead to mistakes. Tags are also the best way to have a list of `FName`'s that are available in both C++ and blueprints
- Any signal processor that utilizes this system is referred to as `Input signal processors` by `AIF`'s style guide.
