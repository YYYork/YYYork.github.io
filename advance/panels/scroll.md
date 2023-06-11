---
sidebar_position: 5
---

# 滚动窗面板

滚动窗面板是将一些配置好的图标列按顺序展示，支持纵向、横向滚动以查看更多内容的特殊面板

## 声明

除了常规面板通用的属性外，生成器面板具有一个独立的配置节点  
通过此节点可以声明一个滚动窗面板

| **节点**     | 接受值    | 描述          |
|------------|--------|-------------|
| **scroll** | Object | 声明滚动窗面板相关设置 |

## 属性

下列属性均为 `scroll` 节点下的

| **节点**        | 接受值    | 描述                  |
|---------------|--------|---------------------|
| **direction** | String | 滚动方向（默认为HORIZONTAL) |
| **tail**      | Int    | 尾巴                  |
| **colums**    | List   | 滚动栏目                |

- `direction` 可选的值有
    - `horizontal` 水平
    - `vertical` 垂直
- `tail` 决定滚动如何收尾
    - `tail = 0` 停在最后一个栏目（不展示空白）
    - `tail > 0` 展示 `tail+1` 个空白栏目
    - `tail < 0` 循环无缝衔接滚动
- `colums` 是配置滚动栏目元素

## 滚动窗

你需要通过 `Layout` 来定义滚动窗，方法是在 Layout 中留下一个空白的矩形

例如配置

```yaml
layout: |-
  <       >
```

则滚动窗为定位在 `[1, 0]`，大小为 `7x1` 的窗口  
滚动窗的大小和滚动方向将决定元素栏目配置的上限

### 水平滚动

对于水平滚动的窗口，每个滚动栏目应包括`滚动窗高度个`元素  
例如 `7x5` 的窗口，每个栏目应至多包括 `5` 个元素，每个栏目的元素是从上往下依次排列

### 垂直滚动

对于垂直滚动的窗口，每个滚动栏目应包括`滚动窗宽度个`元素  
例如 `9x6` 的窗口，每个栏目应至多包括 `9` 个元素，每个栏目的元素是从左向右依次排列

## 滚动栏目

一个滚动窗口的滚动栏目数量不受上限  
但每个滚动栏目的数量是根据方向分布所受限的

例如，对于水平滚动的面板

```yaml
layout: |-
  <       >
```

其滚动窗大小为 `7x1`，单个栏目的上限为 `1` 个元素  
便可这样配置

```yaml
scroll:
  direction: horizontal
  tail: -1
  colums:
    - [ material: apple ]
    - [ material: golden_apple ]
    - [ material: enchanted golden apple ]
    - [ material: melon slice ]
    - [ material: sweet berries ]
    - [ material: glow berries ]
    - [ material: chorus fruit ]
    - [ material: carrot ]
    - [ material: golden carrot ]
    - [ material: potato ]
    - [ material: baked potato ]
    - [ material: poisonous potato ]
    - [ material: beetroot ]
    - [ material: dried kelp ]
    - [ material: raw beef ]
    - [ material: steak ]
    - [ material: raw porkchop ]
    - [ material: cooked porkchop ]
```

也允许简化写成

```yaml
scroll:
  direction: horizontal
  tail: -1
  colums:
    - material: apple
    - material: golden_apple
    - material: enchanted golden apple
    - material: melon slice
    - material: sweet berries
    - material: glow berries
    - material: chorus fruit
    - material: carrot
    - material: golden carrot
    - material: potato
    - material: baked potato
    - material: poisonous potato
    - material: beetroot
    - material: dried kelp
    - material: raw beef
    - material: steak
    - material: raw porkchop
    - material: cooked porkchop
```

![scroll_panel](/res/demo_scroll.gif)
