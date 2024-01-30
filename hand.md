---
description: The hand module
---

# Hand

This feature lets you put a fake item in the offhand of the player. As the module's name (Hand) suggests, this is usually used to put a fake hand item in the offhand which is specially positioned to look like it is "holding up" the weapon. This is especially convincing for large weapons, or 2 handed weapons.

This can also be used for scope reticles.

{% hint style="info" %}
This feature _mirrors_ the [Skin](https://app.gitbook.com/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/skin "mention") module (The config is the exact same). This means that you can use skins and attachments to modify the hand item.

Use `/handskin` in game to change your preferred hand skin.&#x20;

Importantly, the `Hand` section in config **DOES NOT GO IN THE SKIN SECTION**!

> Good

```yaml
AK_47:
  Hand: <...>
  Skin: <...>
```

> Bad

```yaml
AK_47:
  Skin: 
    Hand: <...>
```
{% endhint %}

```yaml
  Hand:
    Default: <integer>
    Scope: ADD <integer>
    Scope_<number>: ADD <integer>
    No_Ammo: ADD <integer>
    Reload: ADD <integer>
    Sprint: ADD <integer>
   
    # This requires WeaponMechanicsCosmetics to be installed
    <skin>: ADD <integer>
    <another skin>: ADD <integer>
    
    # This required WeaponMechanicsPlus to be installed
    Attachments:
      <attachment title>: ADD <integer>
      <another attachment>: ADD <integer>
```

All config options work the same as [Skin](https://app.gitbook.com/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/skin "mention"), check out that wiki for more information.
