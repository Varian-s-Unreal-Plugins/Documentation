---
topic: "[[Projects/Unreal Engine/AIF/Documentation/Agent Intelligence Framework/Agent Intelligence Framework|Agent Intelligence Framework]]"
---
`AIF` has a lot of systems and creating a debugger for each one would have consumed a lot of my time. In an effort to implement acceptable debuggers, `AIF` builds on top of `Mass`'s built-in debugger you can activate with the `'` (tilda) key and from there you can select the entity closest to the center of your screen through `Shift + P`. `AIF` then provides numerous console commands for each system to enable or disable debug code.

To improve debugging, `AIF` utilizes `OmniToolbox`'s draw and log debugging system. This is essentially just a system that combines `Visual Logger` and Unreal's `Draw Debug (shape)` functions.

This means if you enable `Visual Logger` recording while using some `AIF`'s debuggers, you'll be able to rewind and watch what `AIF` was doing and share those logs with others or save them for later comparison.


> [!NOTE] 
> Not all systems have a debugger. Either because they are simple enough that they don't need it, or because I have not found the time to implement it.

## Future of AIF debugging
There's a "ImGui, but for Unreal" being developed by Epic, called `SlateIM`. As of 5.7, it's heavily under development and in my opinion, not really production ready. Once it is more fleshed out, `OmniToolbox` will be creating a generic solution for all of my plugins to create powerful debuggers utilizing `SlateIM`.