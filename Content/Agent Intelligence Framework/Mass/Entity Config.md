---
topic: "[[Mass]]"
publish: true
---
The primary way of creating an entity is through a entity config data asset. There are many tutorials out there that cover this topic, but here are my recommendations and notes.

## Notes
- Parent traits are ignored if the child includes the same trait. As far as I can tell, there is no way for a trait to fetch the parent asset to attempt to merge them.    
    - Entity configs do not behave the same as other classes, like children actors. When you make a child of some actor and modify a property on the parent, it's updated on the child unless the child overrides that property. With entity configs, if you add a trait that the parent has, the parents trait is completely ignored.    
    - This means some traits can be problematic. Take `Assorted Fragments` for example. You might add 5+ fragments in the parent, but the child might only want to add 1 more. You now need to keep in mind that you have to copy everything from parents `Assorted Fragments` to the child and any changes made to the parent have to be manually updated in the children.
        - In general, I do not recommend using the `Assorted Fragments` or `(AIF) Fragments and tags` traits. In my opinion, every fragment and/or tag should be added through a dedicated trait.

## Recommendations
- Traits should not add fragments it depends on if the trait does not modify the fragment in any way, they should just add them as a dependency. This is because if 2 traits attempt to add the same fragment, you'll get an error.
- Use `AIF`'s child of `UMassEntityConfigAsset`, the `AgentEntityConfig`. This child provides some utilities, such as an enhanced version of `Assorted Fragments` trait (`Fragments And Tags` trait, this filters out many useless fragments and tags, and allows you to filter fragments and tags that have either the `AddThroughTrait` or `RuntimeOnly` meta keywords) and allowing `AIF`'s traits to quickly link you to the documentation for the currently added traits
![[Pasted image 20260331162510.png]]

>You might have to re-open the asset after adding a `AIF` trait for the documentation button to update

## Creating custom traits
I personally don't recommend using the fragment initializers. You can find examples by searching `GetMutableObjectFragmentInitializers` inside your IDE. The reason why I don't like this system is because it's not utilized in all scenarios and doesn't get the best support. For example, `FEntityBuilder` as of 5.7 does not support it and fragments that are added through code don't trigger these initializers.

My recommendation is to use observers instead. They cover every scenario, order is controllable, they can be toggled on or off through the project setting and processed on other threads. The only real benefit initializers have (in my opinion) is that you can have variables stored on the trait, and that's it.
