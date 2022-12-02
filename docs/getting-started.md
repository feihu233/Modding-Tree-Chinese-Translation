# 开始使用
欢迎使用模组树(TMT)！本仓库即为一个最基础的模组树游戏。

## 准备 Getting Started
你需要将本仓库下载到本地以进行下一步。如果你打算使用 Github，那么可以 fork 本仓库。这里以下载为基准。

下载到本地的仓库是一个压缩包，需要解压成文件夹。

找到文件夹下的 index.html，右键-打开方式-找到任何一个浏览器打开。正常情况下双击就能打开了（图标是浏览器）。

<details>
<summary>关于 Demo.html</summary>
Demo.html 是字面意义上的示范文件，它引用的 javascript 文件在 js/Demo 文件夹中。  
打开方式如 index.html，删除它和 js/Demo 对项目没有影响。
</details>

若你使用 Github 并 fork 了本仓库，可以使用以下网站浏览你制作的模组树：
* <https://raw.githack.com/[YOUR-GITHUB-USERNAME]/The-Modding-Tree/master/index.html>
注：需要将中间用中括号括起的内容改为你的用户名，也就是你的个人主页网址最后那一段，比如我的就是 feihu233。

### 注意事项
index.html 中引入了一些谷歌字体、js 文件等，如有可能尽量更换成本地版本。

## 简单学习 Making a Mod
### 设置基础信息 Setting up mod info
打开 js 文件夹下的 mod.js 文件，教程中的文件一般都在此文件夹打开。

mod.js 可对整个游戏进行基础设置，有些设置在游戏正式发布后最好不要更改，否则会发生存档丢失等情况。

目前可更改这些内容：
```javascript
let modInfo = {
    name: "模组名",
    id: "yqeslycswj", // 模组ID
    author: "作者名",
    pointsName: "基本点名称",
    // 其它内容...
}
```
ID 要做到与其它人不重复，可在任意 [ID 生成网站](https://www.345tool.com/zh-hans/generator/random-id-generator)随机生成一个。

在测试模组时，应当在游戏设置中关闭离线进度，并且在不测试时应关闭游戏网页，这可以降低出错几率。

### 层 layer.js
layer.js 可以定义游戏中的“层”，文件中已经有一个基本层，你可以对其进行修改，也可以新建一个层。

目前了解这些即可，详细注释将在 layer.js 中翻译：
```javascript
// addLayer 是创建新层的函数，p 是层ID，在之后会使用
addLayer("p", {
    name: "prestige", // 可选不建议，很少用到
    symbol: "声望点", // 在网页显示的层名
    color: "#4BDC13", // RGB 颜色代码，用于显示
    resource: "声望货币", // 对应货币名称 
})
```

### 升级 Upgrade
升级是 TMT 的重要功能，其不仅用于升级，也用于里程碑、可购买物品等游戏机制的构建。

向 layer 添加升级项：
```javascript
addLayer("p", {
    //...
    upgrades: { // 升级
        11: { // 第 1 行第 1 个升级项
            name: "升级项名",
            description: "升级项描述",
            cost: new Decimal(1), // 升级项花费
        },
    }
})
```
此时就可以在网页中看到你的升级项了，但点击升级项后游戏几乎没有任何改变，因为没有设计升级项效果，这些内容被放在了 mod.js 中。

在 mod.js 中找到这个函数，并按下例更改：
```javascript
function getPointGen(){
    if(!canGenPoints()){
        return new Decimal(0);
    }
    let gain = new Decimal(1);
    
    // 加入这个条件判断
    if(hasUpgrade('p', 11)){
        gain = gain.times(2);
    }

    return gain;
}
```
现在你购买这个升级项后，就可以看到声望点加速增长了。

<details>
<summary>Decimal 介绍</summary>
这里的 Decimal 对象，可以使 javascript 的整数超出基本类型的限制，关于这个对象的运算也与基本类型不同，具体使用方法请参考本仓库下其他文章。
</details>

### 升级之升级 Upgraded upgrades
回到 layer.js，为层添加一个新的升级：
```javascript
addLayer("p", { /* ... */ upgrades: {
    // 11: {},
    12: {
        name: "第一行第二个升级项",
        description: "使声望增量与当前声望挂钩",
        cost: new Decimal(2),
        effect(){ // 效果
            return player[this.layer].points.add(1).pow(0.5);
        },
        effectDisplay(){ // 效果显示文本格式化
            return format(upgradeEffect(this.layer,this.id) + "x")
        }
    }
}})
```
这里的 this.layer 绑定的是当前层，this.id 绑定的是当前升级项。

在 mod.js 中则需要加上：
```javascript
function getPointGen(){
    // ...
    if(hasUpgrade("p", 12)){
        gain = gain.times(upgradeEffect('p', 12)) // times 是乘法
    }
    return gain;
}
```

### 第三个升级
再添加一个升级，使点数获取翻倍：
```javascript
addLayer("p", {
    // 11: {}, 12: {},
    13: {
        name: "另一个升级",
        description: "点数获取翻倍",
        cost: new Decimal(5),
        effect(){
            return player.points.add(1).pow(0.15);
        } // display 是可选的
    }
})
```
在 mod.js 中作以下更改：
```javascript
gainMult() {
    let mult = new Decimal(1);
    // 加入这个条件判断
    if(hasUpgrade("p", 13)){
        mult = mult.times(
            upgradeEffect("p", 13)
        )
    }

    return mult;
}
```