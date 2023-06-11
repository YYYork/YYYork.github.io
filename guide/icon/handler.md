---
sidebar_position: 4
---

# 交互

| **节点**     | 别称                     | 描述   |
|------------|------------------------|------|
| **action** | actions, handler,click | 交互动作 |

:::tip
本节动作的应用案例会提前涉及许多 Kether 语句、条件的应用  
如果尚未了解 Kether 也不必担心，后续章节会讲到
:::

## 理解动作

Invero 原生支持的动作包括以下类型

- Kether 动作
- IF 结构动作
- IF_NOT 结构动作
- ANY 结构动作
- ALL 结构动作
- NONE 结构动作
- IF 结构动作
- CASE & WHEN 结构动作
- CATCHER 捕获器功能动作

除 Kether 可以简化为单 String 类型外，其余动作均为 Object 配置结构  
而图标的交互动作配置节点，接受
- String（单 Kether 动作）
- Object （单结构动作）
- List String（Kether 动作集合）
- List Object（任意动作集合）

以下给出每种 "动作" 的配置示例，  
注意这里的 `action` 节点不一定代表图标下的 `action` 节点

```yaml title="String （单 Kether 动作）"
action: |-
  tell "Hello World!"
  menu close
```

```yaml title="Object （单结构动作）"
action:
  if: condition
  then: action1
  else: action2
```

```yaml title="List String（Kether 动作集合）"
action:
  - |-
    tell "Hello World!"
    sleep 1s
    tell "after 1sec"
  - menu title to "{{second}}"
  - menu title update
```

```yaml title="List Object（任意动作集合）"
action:
  - case: second
    when:
      "> 30": 'tell later'
      "< 10": 'tell pre10'
    else: |-
      tell "second in range [10, 20]"
  - if: conditon
    then: action1
    else: action2
```

对于 List 多个动作集合，按顺序执行，  
若任意一个动作的执行值返回 false，则中断后续动作执行


### IF 结构动作

```yaml
if: 'condition'
then: { }
else: { }
```

- `if` 配置条件字符串, `then` 和 `else` 均配置 Invero 动作（支持嵌套）
- 若 `if` 条件通过，则执行 `then` 否则执行 `else`
- `then` 和 `else` 作为反应动作，至少配置其中之一
- 此外还有节点名为 `if_not` 同型结构动作

### ANY 结构动作

```yaml
any: [
    'condition 1'
    'condition 2'
    'condition 3'
]
then: {}
else: {}
```

- `any` 配置 List 条件字符串，若任意一个通过则执行 `then`，否则执行 `else`
- 其余理解与 IF 结构动作 相同
- 此外还有节点名为 `all`, `none` 的同型结构动作

### CASE & WHEN 结构动作

```yaml
case: 'player name'
when: 
  "= Arasple": 'tell 1'
  "= bukkitObj": 'tell 2'
else: 'tell 3'
```

- `case` 配置 Kether 语句，其返回的值通过 `when` 下配置的来判断、执行
- 若 `when` 没有任意节点匹配，则执行 `else` 下的动作

判断操作符（其中 EQUALS 可省略）

```
GREATER_OR_EQUALS(">=", "≥"),

GREATER(">"),

SMALLER_OR_EQUALS("<=", "≤"),

SMALLER("<"),

EQUALS("=", "=="),

EQUALS_IGNORECASE("~=", "~=="),

CONTAINS_IGNORECASE("~~"),
```

:::tip 为什么有 Kether 还要这么多结构动作 ?

纯 Kether 的应用场景是脚本编程式的，配置起来门槛较高且可读性较低  
例如脚本实现的

```yaml
action: |-
  if all [ player op check player level > 30 ] then {
    msg "Condition matched"
  } else {
    msg "Condition failed"
  }
```

通过结构动作则可写为

```yaml
action:
  all:
    - player op
    - check player level > 30
  then: |-
    msg "Condition matched"
  else: |-
    msg "Condition failed"
```

相比而言，后者更加清晰规范，在底层配置逻辑上可读性更高  
除此之外，结构动作还提供诸如 **输入捕获** 这类繁琐的，不易通过 Kether 规范配置的高级动作

当然，具体使用何种配置方式完全取决你自己的喜好
:::

## 声明交互类型

```yaml
action:
  left: 'tell left_action'
  right: 'tell right_action'
  def:
    if_not: condition
    then: 'tell def_action'
```

- `action` 节点下首先配置交互类型的子节点，然后再配置相关动作
- `def` 节点是任何点击类型都会执行的内容