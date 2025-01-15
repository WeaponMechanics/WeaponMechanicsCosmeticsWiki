---
description: The cosmetics module for the weapon
---

# Cosmetics

```yaml
  Cosmetics:
    Muzzle_Flash: <true/false>
    Hit_Marker: <message>
    Death_Messages:
      - <Message>
    Splash_Mechanics: <Mechanics>
    Block_Hit_Mechanics: <Mechanics>
    Bullet_Zip:
      Maximum_Distance: <distance>
      Sounds: <Mechanics>
    Block_Damage:
      Ticks_Before_Regenerate: <ticks>
      Drop_Broken_Block_Chance: <Chance>
      Damage_Per_Hit: <Integer>
      Default_Block_Durability: <Integer>
      Default_Mode: <CANCEL/BREAK/CRACK>
      Default_Mask: <Material>
      Blocks:
        - <Material*> <CANCEL/BREAK/CRACK*> <ShotsToBreakBlock> <Mask>
    Third_Person_Pose:
      Default: <Animation>
      Scope: <Animation>
      Reload: <Animation>
      Firearm_Action: <Animation>
      
```

## Muzzle\_Flash

A fake torch item will be dropped and instantly removed when set to `true`. Players who use [Optifine](https://optifine.net/downloads) will see a brief flash of light from the gun. _PLAYERS WITHOUT OPTIFINE CAN NOT SEE THIS EFFECT!_

If the shooter looks at their feet while shooting, they will probably see this torch for 50 milliseconds. If this bothers you or your users, I recommend setting this to `false`.

Want to use custom model data (or otherwise customize the dropped muzzle flash item)? Use [Mechanics](https://github.com/WeaponMechanics/MechanicsMain/wiki/FakeItemMechanic) instead.

## Hit\_Marker

Spawns a temporary fake armor stand showing how much damage a hit dealt. You can use the `<damage>` variable for the amount of damage rounded to 2 decimal places. You can use [color codes](https://github.com/WeaponMechanics/MechanicsMain/wiki/General#Message-Color-Codes).

Example: `<red><damage>`

## Death\_Messages

When a player is killed by this gun, 1 message is randomly selected from this list. You can use `<source_name>` to show the name of the shooter, and `<target_name>` for the player being killed.

```yaml
    Death_Messages:
      - "<yellow><target_name> was killed by the big iron on <source_name>'s hip"
      - "<rainbow><source_name> didn't care that he was after <target_name>"
```

## Splash\_Mechanics

These mechanics to trigger whenever a projectile from this weapon enters the water. It's nice to have a quick splash sound and splash particle. Uses [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention").

* `@Source{}` -> the current location of the projectile (usually deeper into the water!)
* `@Target{}` -> targets the point the projectile hit the water.

```yaml
    Splash_Mechanics:
      - "Sound{sound=ENTITY_GENERIC_SPLASH, pitch=1.85, noise=0.15} @Target{}"
      - "Particle{particle=WATER_SPLASH, count=20, noise=0.2 0.2 0.2} @Target{}"
```

{% hint style="info" %}
This feature should only be used when the projectile's [Type](https://app.gitbook.com/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/projectile#type "mention") is `"INVISIBLE"`. Projectiles with disguises have splash effects that are automatically added by the vanilla Minecraft client.&#x20;
{% endhint %}

## Block\_Hit\_Mechanics

The mechanics to trigger whenever a projectile hits a block. Uses [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention")

{% hint style="info" %}
WeaponMechanicsCosmetics automatically adds block impact sounds and particles to all weapons depending on the block that is hit. You can configure those settings in <mark style="color:yellow;">**your server -> plugins -> WeaponMechanicsCosmetics -> config.yml**</mark>
{% endhint %}

## Bullet\_Zip

When a bullet flies past your ear, since it is moving so fast, you hear a ["zip" sound](https://youtu.be/ZpCu4bEUuQM?t=163). This adds an essential layer of immersion to your guns... It allows players to "feel" the bullets flying past them.

* `Maximum_Distance`
  * Defines how far away the player can hear the "zip" from.
  * This **MUST** be a small number... Less than eight blocks for best results.
* `Sounds`
  * The [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") to trigger
  * The resource pack comes with a custom sound for this: `fx.whiz`
  * `@Target{}` targets the entity that should hear the sound and the point the projectile zips by at.

```yaml
    Bullet_Zip:
      Maximum_Distance: 4.0
      Sounds:
        - "CustomSound{sound=fx.whiz, noise=0.02, listeners=Target{}} @Target{}"
```

## Block\_Damage

`Block_Damage` allows control over how damage applies to blocks. For example, if you only want blocks to crack instead of break, or if you want blocks like stone/concrete/bricks/etc to take more damage before breaking.

You can change block damage particles/sounds for all weapons in the `config.yml` section.

* `Ticks_Before_Regenerate`:
  * The time, in ticks, before the broken block will regenerate.
  * Delete this line if you don't want blocks to regenerate (This causes permanent damage!).
  * 1 minute = 60 \* 20 = 1200 ticks.
* `Drop_Broken_Block_Chance`:
  * The chance of spawning an item from breaking a block.
  * This probably shouldn't be used with block regeneration (Since the block might regenerate AND drop).
  * Set this to a number between 0% and 100% (**make sure to include the %**)
* `Damage_Per_Hit`:
  * How much damage to deal to the block. Defaults to 1.
* `Default_Block_Durability`:
  * Defines how many hits it takes to break blocks.
  * This can be overridden per block in the `Blocks` list.
* `Default_Mode`:
  * Defines how blocks should be damaged.
  * `CANCEL`: Don't apply any damage to blocks.
  * `CRACK`: Show block cracking animation, but don't break the blocks.
  * `BREAK`: Show block cracking animation, then break the blocks.
  * This can be overridden per block in the `Blocks` list.
* `Default_Mask`:
  * Defines the material used to replace the block.
  * Default value is `AIR`, which breaks the blocks.
  * For paintball-style guns, you could set this to `RED_CONCRETE`.
  * This can be overridden per block in the `Blocks` list.
* `Block_List`:
  * Format is: `<Material> <CANCEL/CRACK/BREAK> <Integer>~<Material>`
  * See Materials for your version.
  * Examples:
    * `- BEDROCK CANCEL` Stops bedrock from being broken
    * `- DIRT BREAK` Destroys dirt with one shot.
    * `- OBSIDIAN CRACK 5` Shows the full crack animation after 5 shots but doesn't break.
    * `- GRAY_STAINED_GLASS_PANE BREAK 1 DIRT` Destroys gray stained-glass panes and replaces it with dirt with 1 shot (`1.13` and higher).
    * `- $glass BREAK 2` breaks all glass block types in 2 shots.

In this example, bedrock, obsidian, and netherite cannot be damaged. Any material that has "glass" in the name is broken in 2 shots, except for any material with "glass\_pane" in the name, which can be broken in 1 shot. Any material with "wood" in the name can be broken in 6 shots, and dirt can be broken in 4 shots. All other materials cannot be broken, but they appear to take 12 shots of damage and show the crack animation. 10 seconds after a block is broken, it is regenerated.

```yaml
    Block_Damage: 
      Ticks_Before_Regenerate: 200  # 10 seconds
      Default_Block_Durability: 12
      Default_Mode: CRACK
      Blocks:
        - bedrock CANCEL
        - obsidian CANCEL
        - netherite_block CANCEL
        - $glass BREAK 2
        - $glass_pane BREAK 1
        - $wood BREAK 6
        - dirt BREAK 4
```

## Crossbow

{% hint style="warning" %}
This feature only works for OTHER PLAYERS who are looking at you. You _CANNOT_ see this effect in the third person. This is due to a Minecraft limitation, and cannot be fixed by us.
{% endhint %}

Valid animation types are: `NONE/EAT/DRINK/BLOCK/BOW/SPEAR/CROSSBOW/SPYGLASS/TOOT_HORN/BRUSH/BUNDLE`. I personally recommend using `BOW`, since it looks like it is aiming the weapon at the crosshair.&#x20;

* `Default`: when the player holds a weapon, but is not doing any specific action
* `Scope`: when the player is zooming in with their weapon
* `Reload`: when the player is actively reloading their weapon
* `Firearm_Action`: when a firearm action open/close is currently in progress
  * I recommend using `CROSSBOW` here, especially for lever action rifles.
