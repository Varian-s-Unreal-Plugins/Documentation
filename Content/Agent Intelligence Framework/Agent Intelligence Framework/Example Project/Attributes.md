---
topic: "[[Example Project]]"
publish: true
---

The example project demonstrates an example of implementing attributes that utilizes `OmniToolbox`'s Float Providers

> [!NOTE]
> This is not the only way of implementing attributes into a project. It's simply my preferred method.

The example's attributes display an example of initializing attributes through float providers. Meaning they can be initialized through data tables, curve tables, or just flat floats.
- The base value for the float providers is automatically assigned to be the entities level (if the level attribute is available). This means that curve tables will automatically scale the attribute based on the entities level.
