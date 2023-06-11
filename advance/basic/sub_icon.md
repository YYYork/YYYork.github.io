---
sidebar_position: 0
---

# 条件图标

条件图标是属于主图标的一个额外属性，  
皆在更规范地实现 "满足一定条件下的显示图标和执行动作"

条件子图标的配置是在**主图标**的根节点下进行的

| **节点**  | 别称    | 描述    |
|---------|-------|-------|
| **sub** | icons | 子图标列表 |

## 子图标属性

除了常规图标具有的属性外，子图标还有额外的属性如下

| **节点**        | 别称      | 接受值    | 描述         |
|---------------|---------|--------|------------|
| **condition** | if,rule | String | 显示条件       |
| **inherit**   | -       | Bool   | 是否继承父级图标属性 |

- `condition` 是子图标必不可少的 Kether 条件表达式
- `inherit` 默认是启用的，减少一些重复的配置

```yaml title=示例
'myCustomIcon':
  material: apple
  name: 'Apple'
  sub:
    if: player op
    material: diamond
    name: 'Diamond'
    action: tell Hello
```

在这个只有一个子图标的示例中，第一次渲染图标时会判断条件

如果满足 `player op`，即玩家是 OP 管理员，则显示材质为 `钻石` 的图标，  
并支持交互时执行动作 `tell Hello`

如果不满足条件，则显示默认的材质为 `苹果` 的图标

## 多级子图标

同样在是在子图标节点写，将各个子图标写成 `List` 的格式即可

```yaml title=示例
rank:
  material: stone
  name: 'Unranked'
  sub:
    - rule: perm "group.vip+"
      material: emerald
      name: 'VIP+'
    - rule: perm "group.vip"
      material: diamond
      name: 'VIP'
```

此示例中的判断顺序是从前往后，即先判断 `VIP+`，再判断 `VIP`  
如果均不满足条件，则显示默认的 `Unranked`