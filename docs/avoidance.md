#Avoidance
##Dodge and Parry

Both Dodge and Parry work in the same way and characters by default will have 3% chance to do either, however this is reduced by 1.5% for each level difference. Against a target 1 level higher a player will have 1.5% of each, and 2 levels higher (Dungeon Bosses) = 0%, and level 63 (Raid Bosses) = -1.5%.

$$
Diminished\:Avoidance\:Chance = \frac{Bonus\:Avoidance\:Chance} {(Bonus\:Avoidance\:Chance*v+h)}
$$

By default the value of v is **0.01** and the value of h is **1/0.94**.

To calculate ones bonus avoidance chance, one must first find their bonus primary stat as well as their crit rating

$$
Bonus\:Avoidance\:Chance\:=\:\frac{Bonus\:Primary}{P}\:+\frac{Crit\:Rating}{D}
$$

At level 60, P is **138.75176305** and D is **39**


##Class Differences

Different classes can have different values from the standard v and h


Demon Hunter V is **0.02**