# 层(layer)机制解析 Basic layer breakdown

这是一个最小化的层实例，使用了最少的特性。
```js
addLayer("p", {
// 返回 layer 的默认数据，可以在这里设置绝大多数变量
startData() { return {
    unlocked: true,
    // 可以为资源指定名称
    points: new ExpantaNum(0),
}},
// 颜色，影响很多元素的表现
color: "#4BDC13",
// layer 所在的行，以 0 为第一行
row: 0,
// The name of this layer's main prestige resource.
resource: "prestige points",
// The name of the resource your prestige gain is based on.
baseResource: "points",
// 返回 baseResource 的当前数量
baseAmount() { return player.points },

// 
// The amount of the base needed to  gain 1 of the prestige currency.
// 解锁该层需要的资源数量
// Also the amount required to unlock the layer.
requires: new ExpantaNum(10),

// 决定用何种公式计算声望获取
type: "normal",

// 公式系数
// normal 模式的声望获取量 = currency^exponent
exponent: 0.5,

// Returns your multiplier to your gain of the prestige resource.
gainMult() {
// Factor in any bonuses multiplying gain here.
    return new ExpantaNum(1)
},
gainExp() {
// 返回计算声望资源的公式
// Returns your exponent to your gain of the prestige resource.
    return new ExpantaNum(1)
},
// 返回布尔值，表示该层是否会显示在声望树上
layerShown() { return true },
// 参考 upgrades 的文档
upgrades: {},
})
```
