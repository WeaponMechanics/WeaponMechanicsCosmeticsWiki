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

* [Delay\_Between\_Shots](http://127.0.0.1:5000/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/shoot#delay\_between\_shots "mention") -> Useful for semi-auto for burst weapons
* [Shoot\_Delay\_After\_Scope](http://127.0.0.1:5000/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/scope#shoot\_delay\_after\_scope "mention") -> The time players cannot shoot after scoping in.
* [Weapon\_Equip\_Delay](http://127.0.0.1:5000/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/info#weapon\_equip\_delay "mention") -> The time players cannot shoot after equipping their weapons.
* [Reload\_Duration](http://127.0.0.1:5000/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/reload#reload\_duration "mention") -> Total time to complete reload
* [Firearm\_Action](http://127.0.0.1:5000/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/firearm\_action "mention") -> Time to open/close weapon
* [Melee\_Hit\_Delay](http://127.0.0.1:5000/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/melee#melee\_hit\_delay "mention") -> Delay to hit again after hitting a swing
* [Melee\_Miss](http://127.0.0.1:5000/s/nwFaVZ2SN7YPdxsP5G6f/weapon-modules/melee#melee\_miss "mention") -> Delay to hit again after missing a swing

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

* `<time>`: The `x.x` amount of time left. Updates every two ticks.
* `<bar>`: Shows the bar defined by `Bar`. See the example below.

## Item\_Cooldown

Uses the pearl cooldown for your items..\
![pearl](https://user-images.githubusercontent.com/43940682/182694676-26306d42-7015-4b96-83fc-04dc46c11668.png)

{% hint style="danger" %}
Due to Minecraft limitations, this cooldown shows for all items of the same type. This means that if your weapon is a feather, this cooldown will show for ALL feather items.

This effect is only visual, and does not prevent using the item.&#x20;
{% endhint %}

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

* `Message` -> The title of the boss bar. Can use `<time>` and `<bar>`.
* `Color` -> One of `PINK`, `BLUE`, `RED`, `GREEN`, `YELLOW`, `PURPLE`, `WHITE`
* `Style` -> One of `PROGRESS`, `NOTCHED_6`, `NOTCHED_10`, `NOTCHED_12`, `NOTCHED_20`

## Bar

This section replaces all instances of `<bar>` in your messages. It's a nice visual way to show a progress bar without using the `Exp` or `Boss_Bar` feature.

* `Left_Color` -> A message color code, like `<red>`
* `Right_Color` -> A message color code that is **DIFFERENT** then `Left_Color`.
* `Left_Symbol` -> The symbol to use for the bar. I recommend using one character. Try: `|`, or `:`.
* `Right_Symbol` -> If you want to use different symbols, you can use another one character symbol. I recommend skipping this feature.
* `Symbol_Amount` -> The amount of symbols to use in a full bar.

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
