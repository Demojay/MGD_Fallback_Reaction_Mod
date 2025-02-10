# Monster Girl Dreams - Reaction Fallback Mod
Code Mod to allow the specification of delegate skills for certain reaction types - meaning that the delegate's dialogue will be used for a reaction is the original skill does not have a reaction defined for them.
\
\
This mod has been created for [Monster Girl Dreams](https://threshold.itch.io/monster-girl-dreams) v26.8a.

## Reaction Types Supported
- HitWith
- AutoCounter/AutoCounterSkill
- AutoCounterSkillTag
- AutoCounterSkillFetish
- PlayerRecoil/PlayerRecoilA
- HitWith/HitWithA
- HitWithPre

## Installation
Copy the game folder included in the download into the main MGD game folder

## Usage
In order to define a delegate for a particular, a key called "reactionFallback" needs to be added via a JSON file. This can be done as part of the original definition of a skill JSON, or using
the base game's JSON addition system.
\
\
This key will be associated with an object, which contains string/string pairs - the reaction type that the delegate skill will be used for, and the name of the delegate skill to be used.
\
\
The following keys are valid for the "reactionFallback" object (along with the reaction types the key refers to):
- hitWith (HitWith)
- hitWithPre (HitWithPre)
- playerRecoil (PlayerRecoil/PlayerRecoilA)
- autoCounter (AutoCounter/AutoCounterSkill)
- autoCounterTag (AutoCounterSkillTag)
- autoCounterFetish (AutoCounterSkillFetish)

\
An addition key ("all") can also be used which will act as a catch-all delegate skill for reaction types. If an explicit reaction type has not been defined for the "reactionFallback" object,
but an "all" key/value pair has been added, that delegate skill will be used by default. If both a specific reaction type and an "all" pair has not been included in the object, no delegate actions will
be used at all, and functionality will be carried out similarly to the base game.

## Example
```
...
  "reactionFallback": {
    "all": "Arousero"
  }
}
```
\
This example specifies the move "Arousero" for all types of reactions for the skill. When the original move is used to hit a monster, the mod will check to see if there is at least one
reaction defined for "HitWith" for the orignial skill, only those reactions will be displayed. If there are no reactions defined for the original skill, the "HitWith" reactions for the 
Arousero skill (the delegate) will be used instead. If the delegate skill does not have any "HitWith" reactions defined as well, no reactions will be displayed (the mod does not check
 recursively). 
\
\
\
```
...
  "reactionFallback": {
    "all": "Arousero",
    "hitWith": "Mass Seduction"
  }
}
```
In this case, when the system is looking for "HitWith" reactions, and the original skill does not have reactions defined for it with the current monster, the reactions defined for the "Mass Seduction"
 skill will be used instead, since it has a higher priority then the delegate key defined by the "all" key.
