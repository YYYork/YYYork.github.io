---
sidebar_position: 7
---

# 事件

```yaml title=结构
events:
  # 开启前执行的动作
  pre_open: { }
  # 开启后执行的动作
  post_open: { }
  # 关闭时执行的动作
  close: { }
```

- 如果 `pre_open` 返回 `false`，则菜单不会开启
- 这里的节点配置的动作是属于结构动作，同样支持多种写法