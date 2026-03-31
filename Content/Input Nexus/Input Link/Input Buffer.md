---
publish: true
topic: "[[Input Link]]"
---
# Input Buffer
Each `InputNexus` can temporarily suspend events to `InputLinks` that enable input buffering.

Buffers are separated by `InputBufferChannels`, which is a TMap of gameplay tags and `InputLinks`. When the channel is opened, this buffer is populated by any links that attempted to be activated but were stopped, while also storing the last action value.

When the channel is closed, the `InputLinks` will act as if the player just pressed the button, but using the last stored action value that was used.
* Keep in mind, this is not a queue system. Only the last input event will be repeated.


> [!NOTE] Note
> To open a buffer channel, call `OpenInputBufferChannel`, then to close it, you call `CloseInputBufferChannnel`.

Inputs are buffered inside `UInputLink` ➝ `BufferInput`. If you wish to override or customize how a link handles buffering, override this function.

Once the channel is closed, all the inputs are released like so:

![[Pasted image 20260331195717.png]]

Do note, this follows the same code execution as when an input is pressed, as in, checking if it's enabled, can handle the input and consumption

> [!WARNING] Warning
> If you have the `InputLink` trigger on the `Completed` event, the released buffered input might not trigger the way you'd expect.
> 
> Since the `Completed` event can reset the input value, that means the data inside of `FInputActionValue` will be null.

To cancel an `InputLink`'s buffered input, call `FlushBufferedInput`<br>

## Animation based buffering
`InputNexus` provides an animation notify state that allows you to open and close a input buffer channel

![[Pasted image 20260331195725.png]]

When it starts, the buffer channel is opened. When it ends, the buffer channel is closed.

![[Pasted image 20260331195732.png]]