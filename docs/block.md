# Block

## Chance to Block

Block chance is primarily gained from the mastery of Protection Paladin and Protection Warrior.
The formula is the following.

$$
Final\:Block\:Chance = Base\:Block\:Chance\:+\:Bonus\:Block\:Chance+\:Flat\:Modifiers
$$

$$
Bonus\:Block\:Chance = \frac{Mastery\:Bonus\times X}{Mastery\:Points \times X \times v + h}
$$

Protection Paladin has **X** to be 1, while Protection Warrior has **X** to be 0.5

Your base block chance is always 10%. This is true for anyone who has the ability to block.

Flat modifiers are things such as [Holy Shield](https://www.wowhead.com/spell=152261/holy-shield), which increases your chance to block by 15%.


## Block Value
Blocking attacks causes them to deal reduced damage, this damage reduction is based on your block value.
This form of damage reduction is hard capped at 85%. 

$$
\frac{block\:value}{block\:value+k}
$$



## K Value

K is a dynamically changing value that depends on the mob attacking the player and was added in BFA.

| Difficulty | K Value|
| --- | --- | 
| Base/open world |  2500 | 
| Season 1 M0/M+ |  2455 | 
| Castle Nathria LFR | 2500 |
| Castle Nathria Normal | 2662.5 |
| Castle Nathria Heroic | 2845 |
| Castle Nathria Mythic | 3050 |
| Season 2 M0 | 2785 |
| Season 2 M+ | 2845 |
| Sanctum of Domination LFR | 2845 |
| Sanctum of Domination Normal | 3050 |
| Sanctum of Domination Heroic | 3282.5 |
| Sanctum of Domination Mythic | 3545 |
| Season 3 M0 | 3172.5 |
| Season 3 M+ | 3282.5 |
| Sepulcher of the First Ones LFR | 3282.5 |
| Sepulcher of the First Ones Normal | 3545 |
| Sepulcher of the First Ones Heroic | 3842.5 |
| Sepulcher of the First Ones Mythic | 4175 |