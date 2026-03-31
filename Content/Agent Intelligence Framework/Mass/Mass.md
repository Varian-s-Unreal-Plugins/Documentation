---
publish: true
topic: "[[Agent Intelligence Framework]]"
---

The primary framework AIF uses to run its gameplay logic is through Mass, an ECS that is possibly going to become the future of all Unreal Engine gameplay development.
While Mass provides amazing features and performance, there are a few notes you must keep in mind before delving further:
Mass is still under development. It's out of beta, but we are still seeing many changes and additions coming in every engine version.
Mass is entirely C++ with very little native blueprint support. All blueprint support I've added is subject to change if Mass ever introduces any blueprint support.
There are very few quality-of-life features within the editor, the majority seem to be limited to C++. (for example, if an entity is missing a fragment required by a state tree, there is no UI indicator telling you what is missing and the entity config doesn't properly communicate what fragments and tags a trait will *actually* add to your entity and there's no debugger for entity relations)
Mass does do a good job of communicating certain issues through the output log. You'll want to go into the filters and search for "Mass".
While AIF provides some blueprint functionality, staying in C++ will always be faster, and using these features is not as efficient as following the traditional Mass workflow. Consider this setup a middle ground of blueprint support, with blazing fast Mass speed
Learning sources
With Mass being so young and very few tutorials around, I've gathered a list of all useful Mass learning sources I could that I've used for both my learning of Mass, but also research for this plugin.
Your first 60 minutes with Mass
Mass Framework for crowds & traffic simulation in Unreal Engine
Megafunk Mass Community Sample
State Tree Course
It covers non-mass state tree's, but all the concepts are the exact same. In Mass, you're just doing everything in C++ and instead of using UCLASS, you're using USTRUCT and doing some things slightly differently.
Remember, Mass is just Unreal's version of a ECS. Meaning discussions from other ECS systems can sometimes be useful, such as this Overwatch GDC talk about their ECS architecture.
X157 Dev Notes
At the bottom of the page are more Mass resources
MassAPI Plugin
Provides many blueprint nodes and functions to work with Mass at a blueprint level. The github and the documentation also cover many "Do's and Don't's" within Mass.
As of writing, this plugin is the best at providing blueprint support to Mass.
Hytale's ECS explained
The first 15 minutes are a great explanation of the differences between OOP and ECS.
Mass notes
Many Mass functionalities, such as the gameplay tags system is executed at the end; or the beginning of the next frame. This might make some blueprint code confusing. For example, if you call AddTagsToEntity, then try to print it immediately, the tags won't appear in the message. But on the next frame, they will be.
In general, this is how many ECS's function, they defer their logic either to the end of the frame or the beginning of the next frame. If you're going to use Mass, you'll have to get used to this.
I suggest reading this page for more information
Blueprint support
In the first few weeks of developing this plugin, I really tried to provide a great blueprint user experience, including having developed a blueprintable mass processor. But ultimately, I've leaned back from this for a few reasons:
If you need Mass performance, you need to learn *some* C++. To use Mass, you do not need to understand too much C++ as most processors are very similar and simple. Once you've made 2-3 processors, you got the idea. You can get away with Mass with basic level C++. Some AI assistant tools, such as ChatGPT, have even started writing competent Mass code. (Just be aware that it can hallucinate sometimes)
Many fragments in the engine aren't blueprintable. I've made some functions for the most common fragments, such as GetTransformFragment, GetAgentRadiusFragment, etc. Making your own is very simple and the plugin provides plenty of examples.
Mass is not designed to be used in Blueprints and thus, it's a constant uphill battle against its developers. I would be creating hundreds of wrappers and creating many inefficiencies just to keep up, slowly crippling the performance you would get from Mass.
Creating all these wrappers and workarounds also slows down development time of AIF, when the basics of C++ and Mass can be learned by the average developer in a few weeks to a few months and in the end, that developer will have C++ experience to put on their resume, and their project will perform far better.
Since you have to create mass tags and fragments in C++, you already have to do *some* C++
This might be a hot-take, but the Unreal community has gone on for too long avoiding C++ and encouraging people to only use blueprints, or actively avoid basic or simple C++ and spend hours doing something in far inferior in blueprints. In my opinion, Unreal becomes extremely powerful when you know how to use both C++ and Blueprint. The more blueprint support I add to this plugin, the more I feel like I am becoming part of the problem. If you want to make games and make them well, please, just learn the basics of C++. It's easier than ever before and it's unbelievable how many benefits it brings to you and your project, as there are tons of extremely powerful features that simply do not exist for blueprints.
Ultimately, I've decided to implement blueprint support where it makes sense, make tutorials and list many useful resources so you get the performance of C++ and get better access to Mass's API.
Namespace
Mass uses namespaces for a number of things. The primary is being execution groups. But in the attempt of simplifying Blueprint support, which doesn't have access to C++ namespaces, AIF uses gameplay tags instead to handle naming many things.

Adjusting from "traditional" UE approach to Mass
I want to preface this section by noting that I am not an "ECS professional". Mass is the first ECS framework I've ever interacted with. There are many people on the Unreal Source discord and many other forums who are far smarter than I am and understand ECS's best practices far better than me. Below is essentially just "my take" on going from UE's traditional way of doing things to Mass.
If you're like me, you learned how to do things in the traditional actor and actor component style architecture. This is usually referred to as "object oriented programming", or "OOP".
When I first saw Mass, my first thought was to move all heavy logic to Mass, to better utilize the CPU cache and potentially move some things off of the game thread, but continue doing many things with actor components. But speed is just a neat side-effect of a ECS (entity component system) architecture. It took me a while to look past the speed and that Mass isn't just a fast tool, it's a whole new way of structuring your game.
Let's take an ability system as an example.
With Unreal's traditional approach to creating your game, you would make an actor component and place it on the actor. This component would be responsible for hosting all ability instances, which would be plain Object's, granting default abilities, etc.
Now, let's say you implement a tag system. You give it useful notifies, maybe even add some data to these tags, maybe even filter what tags can or can't be applied to specific actors. Great, let's make into an actor component and we're off to the races! You make it so your abilities can get the owning actor and now you have access to the owners tags. From here, you could block the ability from activating, such as if the owning actor has a "Stunned" tag, great! 
But... What if you wanted to add the same tag system to your ability? Maybe your ability has several states and you want to easily tell which state its in through tags. It's not an actor, so you either have to refactor your entire tag system, or create a separate tag system just for your abilities, or just use a raw gameplay tag container which might be incompatible with all the utility functions you made. All solutions are messy and annoying to deal with.
With Mass, this process is fairly simple. The owner would get a fragment and each ability would be turned into an entity and that fragment references those abilities. That tag system? It's a fragment, so the owner and ability just re-use the exact same system. Basically, imagine if actor components didn't have that "actor" limit associated with it and actors were virtuall free to spawn.
In Mass, everything is shareable, the only limits are what you build into it. It can even easily circulate into itself. That ability is now an entity, so you could now give that ability entity... An ability fragment! Maybe you have a "Place Turret" ability, which spawns an indicator to place a turret. Your "Place Turret" ability could have a "Spawn Turret" ability that is triggered when an input is pressed.
Once you reach the stage of where you have several fragments that do things in fairly abstract ways and are able to chain them in ways that create new systems, it truly feels like you can just do anything, and you never have to make duplicates of anything ever again.
For me, this epiphany happened when I wanted to "stun" an entity. I have a tag system that's applying the "Stunned" tag, I have a fragment that applies a lifetime to an entity (originally made for my projectile entities), so what if I give that tag an entity? I make an observer that when this entity is destroyed, it removes the tag from the owner and now I just give it the "lifetime fragment" and it automatically removed the tag once the entity died! A whole new system was born through just one simple step and reusing existing data. Now, I could apply any tag to any entity temporarily or associate any other data to that tag.
The speed of Mass is great and honestly, too many people focus on just this aspect, but this way of structuring a game is fantastic. I've started using fragments and tags for systems where I know I don't need the speed of Mass.

Current limitations of Mass
Epic has not provided any examples of saving and loading entities. There are some examples out there, but they are nowhere near as rigororous as other saving and loading systems designed around UObject's. There is a lot of code suggesting that Epic is working on it, but if your game heavily depends on this feature, then it might not be time for you to jump into Mass quite yet.
AIF will not be providing any serialization support until Epic provide more information around this.
Ji-Rath has a example plugin showcasing some level of entity saving and loading, though it's very limited. From what I understand, it doesn't restore relations nor tags, and each fragment you'd want to restore would have to be implemented by hand. In the example, it's hard-coding the restoration of the transform fragment. This is what I mean by "nowhere near as rigorous" as other solutions for UObjects. There, you can just label a property as Save Game and that's it. Pointers can be restored and even delegates can be restored. UObject's are just simply far more mature when it comes to saving and loading.
From my research, it's not actually common to try and save and load entities and you're more or less meant to "reconstruct" entities, not "restore" entities.
