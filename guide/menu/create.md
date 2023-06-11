---
sidebar_position: 2
---

# 创建

本节我们将通过创建一个名为 `spawn` 的菜单来演示 Invero 的基本菜单逻辑  
需求是实现以下功能
- 一个 5 行高的箱子容器，周围用两种不同颜色的玻璃板装饰
- 中心一个材质为信标的按钮
- 按钮点击后，玩家请求回到出生点

---

### 创建文件

首先在工作目录下新建一个后缀名为 `yml` 的文件  
并用文本编辑器打开

```yaml title="workspace/spawn.yml"
# 这是一个空文件
```

---

### 声明菜单

1. 设置菜单的标题
```yaml title="workspace/spawn.yml"
title: 'Spawn'
```

2. 想象菜单的布局，并通过字符表示

```yaml title="workspace/spawn.yml"
title: 'Spawn Menu'

layout: |-
  #########
  |       |
  |   *   |
  |       |
  #########
```

:::note 理解布局

Layout 在这里我们配置了 5 行字符串，每行都有 9 个字符  
每个字符都代表箱子槽位上的一个物品，
一共三类字符 `#` `|` `*` 均是我们之后需要配置的图标

而图标在菜单中的实际位置也和布局的字符一一对应
:::

3. 配置简单的装饰性图标

```yaml title="workspace/spawn.yml"
# .. 略去了 title 和 layout 节点
items:
  '#':
    material: gray stained glass pane
  '|':
    material: cyan stained glass pane
  '*':
    material: beacon
```

4. 配置回城按钮

```yaml title="workspace/spawn.yml"
# .. 略去了前面的节点
  '*':
    material: beacon
    # 配置自定义物品名称
    name: '&c&lCLICK TP TO SPAWN'
    # 点击 action 节点
    # 写入 执行回城命令 的动作
    action: command spawn
```

### 查看菜单

- 菜单配置完成后，执行 `invero reload` 即可重新加载工作空间
- `workspace/spawn.yml` 文件的菜单名会是 `spawn`，
- 我们再在游戏中执行 `invero open spawn` 即可查看此菜单

![preview](/res/ui_spanw.png)

:::tip 提示
此案例中的 `声明菜单` 概念是经过简化的，  
详细参阅 [单面板简化写法](./structure#单面板简化写法)
:::