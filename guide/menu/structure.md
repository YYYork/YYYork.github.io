---
sidebar_position: 1
---

# 结构


### 菜单结构

下面是一个标准的 Invero 菜单结构分布  
在实际应用中，较简单的菜单并不会严格按照此结构来配置  

```
myCustomMenuStructure
├─ menu ·················· 声明菜单
│    ├─ type ············· 容器类型
│    ├─ rows ············· 箱子行数
│    ├─ title ············ 容器标题
│    ├─ virtual ·········· 是否启用虚拟容器
│    └─ option ··········· 其他菜单选项
├─ panels ················ 菜单面板
│    └─ standardPanel ···· 示例标准面板
│           ├─ icons ····· 图标
│           ├─ layout ···· 布局
│           ├─ locate ···· 定位
│           └─ scale ····· 尺寸
├─ bindings ·············· 菜单绑定
├─ events ················ 菜单事件
├─ nodes ················· 菜单节点
└─ tasks ················· 菜单周期任务
```

### 面板概念

面板（Panel）可以理解为一个一个独立的 "小菜单"  
其具有自己独立的大小（长 x 宽）、布局、图标以及功能  

一个菜单可以有一个窗口本身大小的面板，  
也可以是多个具有独立功能、目的的小面板组成的  

根据功能，Invero 原生提供以下面板
- 标准面板
- 多页面板
- 生成器面板
- 滚动面板
- 交互槽面板

:::tip 总结
对于复杂、多功能的菜单工程，面板概念可以极大的提高配置管理以及复用效率  
:::

### 多态序列化

Invero 的几乎所有配置节点都支持多态序列化，简单理解如下
- 单节点多别称
- 单节点多写法

例如，在配置菜单标题节点时，根据需求有如下两种写法
```yaml title=静态标题
title: 'My Custom Title'
```

```yaml title=动态标题
title:
  mode: reversable
  period: 20
  values:
  - 'My custom title'
  - 'Reversable'
  - 'Animated title'
```

又例如，在配置动作交互时

```yaml title=单文本Kether语句
action: 'tell Hello_World!'

action: |-
  tell "Hello world!"
  menu title update
  icon by 'headIcon' refresh
```
```yaml title=单结构动作
action:
  if: eco has 500
  then: |-
    eco take 500
    tell 'Took 500$ from your account.'
  else: |-
    tell 'You dont have enough balance.'
```
```yaml title=多动作
action:
  - 'tell Hi'
  - if: eco has 500
    then: |-
      eco take 500
      tell 'Took 500$ from your account.'
    else: |-
      tell 'You dont have enough balance.'
```
以上动作写法并非全部，你也暂时无需理解以上动作的含义，后续章节会详细讲解

### 单面板简化写法

按照标准 Invero 结构来进行配置，需要配置很多个节点
示例如下

```yaml
menu:
  title: 'Spawn Menu'
  rows: 5

panel:
  - layout: |-
      #########
      |       |
      |   *   |
      |       |
      #########
    items:
      '#':
        material: gray stained glass pane
      '|':
        material: cyan stained glass pane
      '*':
        material: beacon
        name: '&c&lCLICK TP TO SPAWN'
        action: command spawn
```

由于本需求中只使用了单个面板，我们可以简写为如下形式

```yaml
title: 'Spawn Menu'

layout: |-
  #########
  |       |
  |   *   |
  |       |
  #########

items:
  '#':
    material: gray stained glass pane
  '|':
    material: cyan stained glass pane
  '*':
    material: beacon
    name: '<red><bold>CLICK TP TO SPAWN'
    action: command spawn
```

可以看到，针对单面板的菜单，面板本身的所有节点和菜单配置的所有节点都可以移动到根节点下  
建议仅在多面板、复杂菜单工程的需求下使用标准的配置结构

本文档 `入门` 章节的菜单配置都将使用简化后的单面板格式

:::tip 你知道吗?
Icon 的底层设计也是分为 `display` 和 `action` 等多部分节点的  
本文档不会对此进行赘述，一律采用简写形式
:::