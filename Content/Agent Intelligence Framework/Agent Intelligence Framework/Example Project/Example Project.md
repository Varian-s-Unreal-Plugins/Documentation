---
topic: "[[Agent Intelligence Framework]]"
publish: true
---

`AIF`'s example project is built on top of Unreal's `Game Animation Sample Project` (or `GASP` for short) as I think it's the best template Epic provides. But I've removed many uneccessary assets (in order to reduce disk size and complexity) and made some small tweaks.

## Structure
Due to `GASP`'s structure, it's very difficult to migrate its assets into a plugin. So `AIF`'s example project is slightly different from `IFP`'s, which some of my current customers might be used to.

The content folder in the example project is entirely `GASP`. All assets found in there belong to Epic Games and are not made by me. They are all freely available on Fab.

The example project contains all example assets in the plugins folder.
- `AIF_CommonAssets`; Common assets shared by all AIF Example project plugins. Such as, gameplay tags, attributes, etc.
- `NameplatesFeature`; Demo of `AIF`'s game feature integration. This gives certain entities a widget 

## Migrating
I personally NEVER recommend anybody ever build their new game on top of an existing template. Be it a template from Epic, or Fab, or somewhere else. You should be reviewing everything that goes into your project.

The example project is an EXAMPLE. It's NOT something you should be downloading, then renaming it to your games name, then starting your games development. You should be using it as an... Example.

## Notes
- I do not want to invest too much time on the example project. This means that some things, such as animations, SFX or VFX for things like abilities is not implemented.
    - I want to invest time in providing a clean and easy to understand implementation of `AIF`'s features.
    - I'd rather invest time in making the plugin itself better.
    - The example project is using assets that are outside of my control. For example; `GASP` is using animation blueprints in 5.7 and it seems that in 5.8, `GASP` will be using `Unreal Animation Framework` (`UAF`). If I were to implement things like animations, I'd just be wasting time trying to customize a system outside of my control. People are familiar with `GASP`, I'm not going to complicate it any further.
