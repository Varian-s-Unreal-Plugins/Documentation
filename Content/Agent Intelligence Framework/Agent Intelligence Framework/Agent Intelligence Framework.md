---
publish: true
---

The Agent Intelligence Framework (AIF) is a plugin that provides a robust framework to build your game using Mass, State Tree's, Smart Objects and more.

- An agent refers to an entity, actor, object, it doesn't mean any unique thing. It's an umbrella term to put all of UE's ways of managing gameplay code into one word.
- While Mass is often associated with AI logic, this plugin brings many features that are abstract from just AI and can be utilized on the player, abilities, static scene actors and more.

> [!WARNING]
> This plugin heavily utilizes Mass, which is a C++-first framework.​

Read the introduction section for Mass to better understand how this plugin supports blueprint.


## Navigating the documentation and source code
This plugin covers many new systems and thus, the documentation might be a little "overwritten" as not everyone has adjusted toe UE's new tech-stack.
Each section has an introduction page, which I highly recommend you go through first before diving any deeper into any section.
The source code organizes every aspect of the plugin into its owner folder. For example;
- The visualizer system is contained inside the `AgentVisualizer` folder.
- The Entity Controller system is contained inside the `EntityController` folder.
This leans away from some other folder structures where you may for example have all processors in one folder, then another folder for all fragments, another for subsystems, etc.

This documentation will be slightly different from my typical type of documentation, due to how young most of the systems this plugin covers, there's very few resources for people to learn how most things work, and not everyone has the same talent I do for reverse-engineering the engine source code.

Because of this, there may be some pages and sections that cover how some plugins work in a more "tutorial" style writing over basic engine features, such as how to set up a Mass entity config, or setting up SmartObjects.

Nearly every property and function have comments. If you're in the editor, you can hover over variables, functions, state tree tasks and so forth to get a tooltip which often shares very important information.