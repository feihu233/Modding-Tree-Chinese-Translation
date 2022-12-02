# 基本信息
模组树中几乎所有的值都既可以是常量，也可以是变量，但变量通常通过函数返回值来表现。你可以将其理解为软性的“不可变”数据。

模组中所有涉及显示文本的字符串值都可以写入 HTML 元素，但不可使用 Vue 特性。

**关键字**：
* 无标签(No label)：如果不包含它们，游戏将崩溃
* 可能需要(sometimes required)：如果你使用了某些机制，那么不包含它们游戏将崩溃
* 可选的(optional)
* 自动分配(assigned automagically)：这个值会自动设置，并覆盖你设置的内容
* 弃用的(deprecated)：已有更好的替代方案

## 超大数
模组树使用 [break\_eternity.js](https://github.com/Patashu/break_eternity.js) 来使用并存储数字，因此这里使用的数字实际上都是 `OmegaNum` 对象，它可以使用类似 `new OmegaNum(1)` 的形式来创建，参数也可以是字符串。

`OmegaNum` 无法使用 javascript 原生的运算符进行运算，而是通过函数进行运算，相关内容请查阅[break\_eternity.js 文档翻译](/docs/omegaNum.md)。


## js 目录（暂存）
* [layers.js](/js/layers.js) 是主要增加游戏内容的文件
* [components.js](/js/components.js) 可以增加新的 Vue 组件，深度定制游戏
* 

## 内容列表 Table of Contents
### 常规 General

- [Main mod info](main-mod-info.md): How to set up general things for your mod in [mod.js](/js/mod.js).
- [Basic layer breakdown](basic-layer-breakdown.md): Breaking down the components of a layer with minimal features.
- [Layer features](layer-features.md): Explanations of all of the different properties that you can give a layer.
- [Custom Tab Layouts](custom-tab-layouts.md): An optional way to give your tabs a different layout. You can even create entirely new components to use.
- [Custom game layouts](trees-and-tree-customization.md): You can get rid of the tree tab, add buttons and other things to the tree,
    or even customize the tab's layout like a layer tab.
- [Updating TMT](tutorials/updating-tmt.md): Using Github Desktop to update your mod's version of TMT.

### 一般组件 Common components

- [升级](upgrades.md)
- [里程碑](milestones.md)
- [可购买物品](buyables.md)
    + [可点击物品](clickables.md)
- [成就/进度](achievements.md)

### 其它组件和特性 Other components and features

- [挑战](/docs/其他组件和特性/challenges.md)：为层创建挑战
- [Bars](bars.md)：使用进度条、显示信息Display some information as a progress bar, gauge, or similar. They are highly customizable, and can be horizontal and vertical as well.
- [Subtabs and Microtabs](subtabs-and-microtabs.md): Create subtabs for your tabs, as well as "microtab" components that you can put inside the tabs.
                        You can even use them to embed a layer inside another layer!
- [Grids](grids.md): Create a group buttons that behave the same, but have their own data. Good for map tiles, an inventory grid, and more!
- [Infoboxes](infoboxes.md): Boxes containing text that can be shown or hidden.
- [Trees](trees-and-tree-customization.md): Make your own trees. You can make non-layer button nodes too!
- [Particle system](particles.md): Can be used to create particles for visual effects, but also interactable things like golden cookies or collectables.
