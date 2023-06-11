---
sidebar_position: 3
---

# 多页面板

翻页的面板的实现渠道。

## 属性

| **节点**           | 接受值           |     | 描述          |
|------------------|---------------|:----|-------------|
| **locate**       | String / Int  |     | 面板的定位（槽位写法） |
| **layout**       | String / List |     | 面板的布局       |
| **scale**        | ListInt       |     | 尺寸          |
| **default-page** | Int           |     | 默认页码        |
| **pages**        | ListPanel     |     | 多页面板        |

## 示例

```yaml
title: 'Demo'
rows: 3

pageController: &page
  material: arrow
  name: '&aPage Controller'
  lore: |-
    Page: {{page get}} / {{page max}}

    &eLeft next
    &6Right previous
  action:
    left: page next icon by '>' refresh
    right: page previous icon by '>' refresh

pages:
  - layout: |-
      #########
      ---------
      ########>
    items:
      '#':
        material: diamond
      '-':
        material: emerald
      '>':
        <<: *page
  - layout: |-
      ##---####
      ##---####
      ##---###>
    items:
      '#':
        material: gold
      '-':
        material: emerald
      '>':
        <<: *page
  - layout: |-
      ######---
      #########
      ---#####>
    items:
      '#':
        material: leaves
      '-':
        material: emerald
      '>':
        <<: *page
```

![paged_panel](/res/demo_paged_panel.gif)

:::tip
这里的配置文件使用了 YAML 的锚点和引用
如果你不熟悉此类操作，请参阅 [YAML 入门教程](https://www.runoob.com/w3cnote/yaml-intro.html)
:::

:::info 注意
多页面板当前仍存在一定的局限性和不稳定性

对于在功能和内容上毫不相干的菜单，不建议使用多页面板来实现
:::