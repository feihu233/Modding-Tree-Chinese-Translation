# 成就 Achievements

成就类似任务，当玩家满足某些条件时达成，并给予玩家奖励。TMT 的成就系统目前功能较少。

You can make global achievements by putting them in a side layer by making its row equal to "side" instead of a number.

Useful functions for dealing with achievements and implementing their effects:

有用的函数：
- hasAchievement(layer, id)：判断玩家是否达成某个成就
- achievementEffect(layer, id)：如果有，则返回当前成就效果

成就的格式如下：
```javascript
achievements: {
    rows: # of rows,
    cols: # of columns,
    11: { // id，第一个为行第二个为列
        name: "Achievement",
        //...
    },
    //...
}
```

Individual achievement can have these features:

- name: **optional**. displayed at the top of the achievement. The only visible text. It can also be a function that returns updating text. Can use basic HTML.

- done(): A function returning a boolean to determine if the achievement should be awarded.

- tooltip: Default tooltip for the achievement, appears when it is hovered over. Should convey the goal and any reward for completing the achievement. It can also be a function that returns updating text. Can use basic HTML. Setting this to "" disables the tooltip.

- effect(): **optional**. A function that calculates and returns the current values of any bonuses from the achievement. Can return a value or an object containing multiple values.

- unlocked(): **optional**. A function returning a bool to determine if the achievement is visible or not. Default is unlocked.

- onComplete() - **optional**. this function will be called when the achievement is completed.

- image: **optional**, puts the image from the given URL (relative or absolute) in the achievement

- style: **optional**. Applies CSS to this achievement, in the form of an object where the keys are CSS attributes, and the values are the values for those attributes (both as strings).

- textStyle: **optional**. Applies CSS to the text, in the form of an object where the keys are CSS attributes, and the values are the values for those attributes (both as strings).

- layer: **assigned automagically**. It's the same value as the name of this layer, so you can do `player[this.layer].points` or similar.

- id: **assigned automagically**. It's the "key" which the achievement was stored under, for convenient access. The achievement in the example's id is 11.

- goalTooltip: **optional, deprecated**. Appears when the achievement is hovered over and locked, overrides the basic tooltip. This is to display the goal (or a hint). It can also be a function that returns updating text. Can use basic HTML.

- doneTooltip: **optional, deprecated**. Appears when the achievement is hovered over and completed, overrides the basic tooltip. This can display what the player achieved (the goal), and the rewards, if any. It can also be a function that returns updating text. Can use basic HTML.

Disable achievement popups by adding `achievementsPopups: false` to the layer.
