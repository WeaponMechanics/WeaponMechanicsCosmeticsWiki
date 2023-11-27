# Show Time

```yaml
  Show_Time:
    Delay_Between_Shots: <Timer>
    Shoot_Delay_After_Scope: <Timer>
    Weapon_Equip_Delay: <Timer>
    Reload: <Timer>
    Firearm_Actions: <Timer>
    Melee_Hit_Delay: <Timer>
    Melee_Miss_Delay: <Timer>
```

Each option here uses the Timer serializer.

* [`Delay_Between_Shots`](https://github.com/WeaponMechanics/MechanicsMain/wiki/Shooting#delay\_between\_shots-integer): Useful for semi-auto or burst weapons,
* [`Shoot_Delay_After_Scope`](https://github.com/WeaponMechanics/MechanicsMain/wiki/Scoping#shoot\_delay\_after\_scope-integer): The time players cannot shoot after scoping in. Useful for heavy sniper weapons.
* [`Weapon_Equip_Delay`](https://github.com/WeaponMechanics/MechanicsMain/wiki/Information#weapon\_equip\_delay-integer): Time time players cannot shoot after equipping their weapon. Useful for heavy weapons.
* [`Reload`](https://github.com/WeaponMechanics/MechanicsMain/wiki/Reloading#reload\_duration-integer): Reload complete time
* [`Firearm_Actions`](https://github.com/WeaponMechanics/MechanicsMain/wiki/Firearms#open): Firearm open/close times.
* [`Melee_Hit_Delay`](https://github.com/WeaponMechanics/MechanicsMain/wiki/Melee#melee\_hit\_delay-integer): Time after hitting an enemy to recharge.
* [`Melee_Miss_Delay`](https://github.com/WeaponMechanics/MechanicsMain/wiki/Melee#melee\_miss): Time after missing an enemy to recharge.

### Timer Serializer

```yaml
    Timer:
      Item_Cooldown: <true/false>
      Exp: <true/false>
      Action_Bar: <Message>
      Action_Bar_Cancelled: <Message>
      Title: <Message>
      Subtitle: <Message>
      Boss_Bar:
        Message: <Message>
        Color: <PINK/BLUE/RED/GREEN/YELLOW/PURPLE/WHITE>
        Style: <PROGRESS/NOTCHED_6/NOTCHED_10/NOTCHED_12/NOTCHED_20>
      Bar:
        Left_Color: <Color>
        Right_Color: <Color>
        Left_Symbol: <Symbol>
        Right_Symbol: <Symbol>
        Symbol_Amount: <Amount>
```

Whenever you see `<Message>`, you can use two additional placeholders:

* `%time%`: The `x.x` amount of time left. Updates every two ticks.
* `%bar%`: Shows the bar defined by `Bar`. See the example below.

## Item\_Cooldown

Uses the 1.9 pearl cooldown for your items. Note that this will show for all items of the same material (but it won't affect anything).\
![pearl](https://user-images.githubusercontent.com/43940682/182694676-26306d42-7015-4b96-83fc-04dc46c11668.png)

## Exp

Use `true` to show the progress in the exp bar. This will not change your experience; it is only visual.

## Action\_Bar

The message to put in the action bar. Can use `<time>` and `<bar>` variables to show the remaining time and the visual timer bar.&#x20;

{% hint style="info" %}
Since each action bar message lasts 2 seconds, you should also use `Action_Bar_Cancelled` when you use `Action_Bar`.&#x20;
{% endhint %}

## Action\_Bar\_Cancelled

The message to put in the action bar if the timer was canceled early. **CANNOT** use `<time>` and `<bar>`.

## Title

The message to put in the title. Can use `<time>` and `<bar>`. The title fades five ticks after the timer completes.

## Subtitle

The message to put in the subtitle. Can use `<time>` and `<bar>`. The subtitle fades five ticks after the timer completes.

## Boss\_Bar

The boss bar is shown at the top of the screen.

* `Message`: The title of the boss bar. Can use `<time>` and `<bar>`.
* `Color`: One of `PINK`, `BLUE`, `RED`, `GREEN`, `YELLOW`, `PURPLE`, `WHITE`
* `Style`: One of `PROGRESS`, `NOTCHED_6`, `NOTCHED_10`, `NOTCHED_12`, `NOTCHED_20`

## Bar

This section replaces all instances of `<bar>` in your messages. It's a nice visual way to show a progress bar without using the `Exp` or `Boss_Bar` feature.

* `Left_Color`: A [message color code](https://github.com/WeaponMechanics/MechanicsMain/wiki/General#message-color-codes).
* `Right_Color`: A [message color code](https://github.com/WeaponMechanics/MechanicsMain/wiki/General#message-color-codes) that is **DIFFERENT** then `Left_Color`.
* `Left_Symbol`: The symbol to use for the bar. I recommend using one character. Try: `|`, or `:`.
* `Right_Symbol`: If you want to use different symbols, you can use another one character symbol. I recommend skipping this feature.

### Examples

```yaml
AK-47:
  Show_Time:
    Reload:
      Item_Cooldown: true
      Action_Bar: "<gray>Reloading %bar% %time%<gray>s"
      Action_Bar_Cancelled: "<red>Reload Cancelled"
      Exp: true
      Bar:
        Left_Color: "<gold>"
        Right_Color: "<gray>"
        Left_Symbol: "|"
        Symbol_Amount: 25
    Weapon_Equip_Delay:
      Item_Cooldown: true
```
