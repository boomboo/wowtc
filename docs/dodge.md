# Dodge

Both Dodge and Parry work in the same way and characters by default will have 3% chance to do either, however this is reduced by 1.5% for each level difference. Against a target 1 level higher a player will have 1.5% of each, and 2 levels higher (Dungeon Bosses) = 0%, and level 63 (Raid Bosses) = -1.5%.

$$
Diminished\:Dodge\:Chance = 3\:+\:Base\:Dodge\:Chance\frac{Bonus\:Dodge\:Chance} {(Bonus\:Dodge\:Chance*v+h)}
$$

By default the value of v is **0.01** and the value of h is **1/0.94**, check the Class Differences to find specifics.

Agility users gain dodge chance by gaining more Agility as well as more Crit.

To calculate ones bonus Dodge chance, one must first find their bonus primary stat as well as their crit rating.

$$
Bonus\:Dodge\:Chance\:=\:\frac{Bonus\:Primary}{P}\:+\frac{Crit\:Rating}{D}
$$

The Base Dodge Chance follows a similar formula as the Bonus Dodge Chance, but without the crit.

$$
Base\:Dodge\:Chance\:= \frac{Base\:Primary}{P}
$$

At level 60, P is **138.75176305** and D is **39**.


## Class Differences

Different classes can have different values from the standard v and h.


Demon Hunter V is **0.02**.
