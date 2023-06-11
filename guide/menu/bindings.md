---
sidebar_position: 6
---

# 绑定

```yaml title=绑定聊天内容
bindings:
  chat: 'content'
```

```yaml title=绑定聊天内容
bindings:
  chat:
   - 'content1'
   - 'content2'
```

```yaml title=绑定聊天命令
bindings:
  chat: '/menu'
```

```yaml title=绑定物品交互
bindings:
  item: 'minecraft:compass'
```

:::info 注意
通过绑定聊天的命令，并不会将命令注册到服务器  
详细的菜单命令注册以及更复杂的物品特征结构会在进阶中解释
:::