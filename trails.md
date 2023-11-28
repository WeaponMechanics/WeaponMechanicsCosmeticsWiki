---
description: Spawn particles behind projectiles
---

# Trails

{% embed url="https://www.youtube.com/watch?v=BbzydkqSgYU" %}
Trails tutorial
{% endembed %}

```yaml
  Trail:
    Distance_Between_Particles: <distance>
    Hide_Trail_For: <distance>
    Shape: <LINE/SPIRAL/POLAR/PARAMETRIC>
    Shape_Data:
      Radius: <distance>
      Points: <amount>
      Loops: <amount>
      Function: <String>
      Cache: <true/false>
    Particle_Chooser: <STOP/RANDOM/LOOP>
    Particles:
      - <Particle1>
      - <Particle2>
      - <etc...>
```

## Distance\_Between\_Particles

This is the distance, in blocks, between each particle spawn. Usually, you want this number to be a little bit less than `1.0`. Using a tiny number like `0.1` may allow you to create a "_perfect line,_" but this will cause both server/player lag.

## Hide\_Trail\_For

This is the distance, in blocks, before the trail starts showing particles. This creates a small gap between the shooter and the trail, so it doesn't cover the player's screen. Defaults to `0.5` blocks. I recommend a value between `0.5` and `1.5`, but you can set these numbers as high as you want.

## Shape

Defines the shape of the trail. For most use cases, you would only ever want to use `LINE`. However, the other options are great for magic/energy weapons.

{% tabs %}
{% tab title="LINE" %}
A straight line of particles, perfectly following the path of the projectile.&#x20;

Takes no arguments.&#x20;
{% endtab %}

{% tab title="SPIRAL" %}
A circle of particles traveling around the path of the projectile. Arguments:

* `Radius` -> Defines how far away from the projectile should the edge of the spiral be.
* `Points` -> Number of points in 1 before repeating the spiral.
* `Loops` -> How many spirals to show at once.&#x20;
{% endtab %}

{% tab title="POLAR" %}
{% hint style="warning" %}
Using Polar functions requires basic knowledge of Calculus.
{% endhint %}

Similar to the [#spiral](trails.md#spiral "mention") option, but lets you use a function for the radius instead of a constant number. Arguments:

* `Function` -> The function, using **theta** as an argument.
  * For example, `Function: "cos(2 * theta)"`
* `Points` -> Number of points in 1 before repeating the spiral.
* `Loops` -> How many spirals to show at once.&#x20;
* `Cache` -> Use `true` to run all the calculations once per reload
  * Only use this if your function "loops back" in a period of $$2\pi$$
{% endtab %}

{% tab title="PARAMETRIC" %}
Lets you define a horizontal and vertical offset.&#x20;

* `Function` -> The function, using **theta** as an argument.
  * For example, `Function: "0.1805 / exp(-theta), 0.0805 / exp(-theta)"`
* `Points` -> Number of points in 1 before repeating the spiral.
* `Loops` -> How many spirals to show at once.&#x20;
* `Cache` -> Use `true` to run all the calculations once per reload
  * Only use this if your function "loops back" in a period of $$2\pi$$
{% endtab %}
{% endtabs %}

## Shape\_Data

* `Radius` -> How far away from the projectile to spawn the spiral particles
* `Points` -> How many points will the circle have? Bigger numbers = more detail. Recommend 16 or higher.
* `Loops` -> How many spirals should we draw at once?
* `Function` -> A polar equation that supports math operations. Try `"2 * cos(4 * theta)"`.
  * If you use `PARAMETRIC`, use a [parametric equation](https://en.wikipedia.org/wiki/Parametric\_equation).
  * Separate two equations with a comma. Try `"0.1805,0.0805"`
  * This also supports equations. Try `"0.1805 / exp(-theta), 0.0805 / exp(-theta)"`
* `Cache` -> Use true to calculate the values once and store them. 99% of the time, you want this to be true.

## Particle\_Chooser

Defines how to choose particles from the following list.

{% tabs %}
{% tab title="STOP" %}
Loop through the particle list 1 time. Once we reach the end of the list, repeat the last particle for the rest of the trail.
{% endtab %}

{% tab title="RANDOM" %}
Always chose a random particle from the list.
{% endtab %}

{% tab title="LOOP" %}
After we reach the last particle in the list, restart from the beginning.
{% endtab %}
{% endtabs %}

## Particles

This list of particles will be spawned to visualize the trail. Check out the [Particle](http://127.0.0.1:5000/s/hz7yMxlL81NxAT44nraH/mechanics/particle "mention") mechanic to learn how to create particles.

### Example

This example spawns 3 smoke particles with some variation every 1 block. This effectively makes small smoke clouds every block.

```yaml
  Trail:
    Distance_Between_Particles: 1.0
    Particle_Chooser: LOOP
    Particles:
      - "Particle{particle=SMOKE_NORMAL, count=3, noise=0.01 0.01 0.01}"
```
