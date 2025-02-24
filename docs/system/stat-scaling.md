# Stats on Gear

## Introduction
The amount of stats on gear is governed by the item budget, that `budget` is distributed to various properties of the item. Though unlike having 100 gold and only being able to spend 100% of it, more than 100% of the `budget` can be spent.

Various stats have their own multipliers to the portion of the budget that goes to a stat. Budget and multipliers are a function of the item level.

For example 'Super Sword' item level 300, has a budget of 307.97915649, 52.59% of the budget goes to strength, 78.89% to stamina and 70% to secondaries; stamina has a multiplier of 1.487644977, secondaries have a mult. of 0.904429862 and strength a mult. of 1.

So said sword would have `307.97915649*.5259*1=161.97` strength, `307.97915649*.7889*1.487644977=361.45` stamina and `307.97915649*.7*0.904429862=194.98` secondaries.

## The Where and the How
All the above values are in the client data (database or text files) as follows

### Budget: RandPropPoints table (rand_prop_points.inc in simc)
This also contains DamageReplaceStat and DamageSecondary, these are used for trinket like effects with scaling -8 and -9
The budget itself is partitioned into Epic/Superior/Good qualities (though they aren't actually used, ie. the 3 qualities are identical) and farther by slots (chest, legs etc.) more on this later.

### Budget distribution: ItemSparse table (StatPercentEditor[..])
StatPercentEditor[..] are percent multiplied by 100 (ie. 5259 means 52.59% percent), the [..] stand for various stats depending on the id.

### Stat multipliers: gametables/staminamultbyilvl.txt, gametables/combatratingsmultbyilvl.txt (sc_scale_data.inc in simc)
As mentioned above these multipliers apply to stamina and secondary stats when converting from budget, these are broken down by slots, however with the exception of jewelry secondary stats all slots have the same multiplier per item level.

### Armor: ItemArmorTotal table
As the name suggests this contains the amount of armor per item level for each armor type (cloth, leather etc.), however this is a 'total' amount of armor for that item level. 'Total' is also somewhat misleading, you can think of it as a base amount for all items for that item level. Each gear slot would use a tiny portion of that amount.

The ArmorLocation table contains the portions per slot. ItemArmorShield contains the amount of armor that is on shields per item level.

### Weapon dps: ItemDamageOneHand and ItemDamageTwoHand tables
Contain weapon dps per item level per quality, though again blue and purple weapon are considered of the same quality and the distinction isn't very important unless you're interested in green/white/gray items.

There are a few other tables that contain budgets for things that don't scale with item level like potions, flasks and similar effects.

## But Why?
So there are thousands of rows of numbers for each slot, item level and quality. A 'natural' question to ask is 'Is there some logic to these numbers, how are they generated?'.
Luckily there is, in fact these numbers are generated by functions and though the functions and processes are not in the database with enough data (which we have) you can derive those.

First a few caveats and notes:

- The functions that generate the data are not 'smooth' for all item levels, in particular values for item levels for previous expansions and item levels for items that are considered 'for leveling' generally use different curves.
- I'll try and keep constants that are likely to change between expansions as arbitrary for generality (`a`, `b`, `c`), and provide the exact values in the appendix.
- Yes 15 does actually mean 15, Blizzard uses 15 as the magic number despite the fact that in Shadowlands a tier is 13 item levels.

Regardless we're going to only look at how stats on items change in the range of item levels used through-out the current expansion tiers (ilvl 200 to 330).

### Budget (**B**)
Budget as a function of item level has the form of \(B(x)=a*1.15^{\frac{1}{15}*x}\), in fact almost every scaling number in the game is driven by that exponential expression (yes even **K**).

- What the above means is that every 15 item levels the budget increases by **exactly** 15%, eg. our 'Super Sword' with a budget of 307.97915649 (at item level 300) would have `307.97915649*1.15=354.1760299635` at item level 315 (that doesn't mean that 13 item levels is exactly 13%, it's actually ~12.87%).

### Stat Multipliers
**Primary** stats (Agility, Strength, Intellect) have a constant multiplier of 1. Which means your primary stats on an item increase by 15% every 15 item levels like budget.

**Secondary** stats have a multiplier that depends on item level, it isn't clear at first glance why the values decrease the way they do. However, working backwards and noticing that generally secondary stats progress linearly with item level it becomes clear that secondary stat multiplier is driven by a function that when multiplied by budget yields a linear expression.

What function when multiplied by `B(x)` produces `bx+c`, simply \(\frac{bx+c}{B(x)}\) and that fits the multiplier data exactly, so in a roundabout way we get that secondaries are driven by `S(x)=bx+c`.
Which means every item level, you get exactly `b` secondary stats regardless of what item level it is. In the case of the 'Super Sword' we don't care what item level it is, for every item level it gains exactly `b` secondaries.
An additional distinction is that jewelry uses a different linear curve than other items.

**Stamina** multiplier is also a function of item level, unlike secondaries however the multiplier increases linearly with item level and we get `H(x)=(bx+c)*B(x)` as the function for the amount of stamina on an item.

This is harder to quantify, but essentially the amount of stamina you gain per item level both depends on how much stamina the item has (exponential) and also increases with item level it also means you gain more stamina throughout the progression than you do primary stat.

**Armor** doesn't use budget, instead the function that drives it is of the form \(a*1.15^{\frac{1}{15}*x}+b\), which is very close to a pure exponential.

**Effects** trinket like effects have their own unique scaling which is similar to stamina in that they are linear * exponential, ie. \((bx+c)*1.15^{\frac{1}{15}*x}\).