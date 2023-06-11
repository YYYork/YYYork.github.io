---
sidebar_position: 6
---

# 菜单语境

每次菜单会话都具有独立的语境，负责存储相关变量  
语境的变量管理是通过 Kether 语句来实现的

## 设置变量

`context set <key> to <value>`

## 取得变量

`context get <key>`

在同一 Kether 脚本环境中，也可以使用 Kether 原生获取变量的动作
`&<key>`

## 删除变量

`context del <key>`

## 是否存在

```
context has <key>
context (no|without) <key>
```

## 数值自增

```
context (inc|increase) <key> by <value>
```

## 数值自减

```
context (dec|decrease) <key>
```

## 注意事项

语境中的临时变量仅在当前菜单会话有效
如果有需要语境中操作持久变量，可参阅 [持久变量](./persist_data)

切换菜单默认会重置语境，若需保留当前菜单的语境请使用 `menu open_ctx` 语句