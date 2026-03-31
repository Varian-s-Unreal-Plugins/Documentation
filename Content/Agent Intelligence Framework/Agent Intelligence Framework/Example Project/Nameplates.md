---
topic: "[[Example Project]]"
publish: true
---
The nameplates found in the example project are a demonstration of `AIF`'s Game Feature integration.

Configuring it is fairly simple, just open the project settings and find the `Nameplates Processor`. From there, you can configure distance and the widget generated.

​

The processor simply finds the player entity via the `FPlayerEntityTag` (found in `AIF_CommonAssets`) and performs a query around that entity.

​

​

## Debuff indicator

​

When an entity with a nameplate has a effect on it with a `Debuff` tag and a `UI Icon` data, it will automatically create a widget to indicate its duration.

​

The circular progress indicator is mostly copied from Epic's `UI Material Lab` example project. If you're looking to recreate it, I suggest migrating `UI Material Lab`'s contents to your project.

​

​

## Notes

​

- ​
    
    The processor is running a hash grid query on the camera location. This means that entities that you want to give a nameplate to must use the hash grid trait and be close to the camera.
    

- ​
    
    First and last names are randomly generated through data tables assigned in the entity name trait.
    

- ​
    
    This system is NOT optimized, it's an example.
