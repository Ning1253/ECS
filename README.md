# Entity Component System

The idea of an Entity Component System is one I did not come up with. 
In fact, I found out about the idea last night while browsing Reddit. 

However, I found the idea so amazingly neat, that I couldn't help but start creating my own implementation!

## Description

An ECS (do I really have to spell it out?) takes the idea of moving away from OOP to its logical conclusion.

In an OOP, the code runs segmented into classes which inherit methods from parents, which hold their own data. 
The first transition away from OOP is to remove the methods from the parents and classes; instead these are replaced with functions, which will operate on all instances in a certain way. 
However, these instances now need to be grouped in certain ways, since they no longer hold their own methods and need to be placed with similar instances to be operated on - a typical fix for this would be implementing eg. a list of all "Cars" and another list of all "Planes" and running the function "drive" on the cars and the function "fly" on all planes. 

Here is where the core idea of ECS sets in - if we already are sorting all our instances into categories, why not just keep the data required for said categories (eg. driving speed, steer control) within the list itself, instead of within the instance?

This creates the idea of the Component, and the function which operates on each set of data within the component is known as the System. 

But of course now the instance holds no methods, and no data, so the reason it is there is to serve as an identifier - so why not abstract the identifier to its bare-bones, and just assign each instance an integer as an identifier?

In fact, since an instance only serves to place its identifier in the Component's list, there really isn't a point to thinking of the instance as anything else than just an integer - let's call that an Entity. 

## Example 

So to recap, an Entity is an integer tag placed in several Components, which are acted on by one or many Systems. So why is this useful?

Imagine an RPG situation, with zombies, and one human, each of which is an entity with a unique ID. Then each zombie can be defined as having: "Health", "Position", "Velocity", "Damage", "Enemy Tracking". The human can be defined to have: "Health", "Position", "Velocity", "Damage", "Control" - the key difference between a human and a zombie is that the zombie automatically tracks its enemy, but the human has controls which he uses to move around. 

So, each Component of "Health", "Position", "Velocity", "Damage" will contain all the zombies, and the human - the "Enemy Tracking" Component will contain the zombies, with their target being eg. the human, and the "Control" Component will contain the human only, with data on what inputs are currently being pressed down. 

Then, the System "EnemyTracker" will run on all entities within "EnemyTrack" and change their positions and velocities based on their targets - and the System "MoveController" will run on all entities within "Control" and change their positions and velocities based on the data there. 

Finally, let's say that the human has a sword, the position of which is dependent on that of the player - one could create a Component "PositionalParent" with the sword inside with a target of "Player", such that the absolute positioning of the sword could be calculated as its "Position" data added to the data of its "PositionalParent". 

Thus, ECS enables us to manage complex webs of entities with functions acting on global scales, and relations between different tables. 

## Implementation

Will be written up at some point, in the future. 