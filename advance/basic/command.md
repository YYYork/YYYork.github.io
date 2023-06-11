---
sidebar_position: 4
---

# 命令构建

## 基础

在菜单的绑定结构下注册服务端命令

```yaml title=简单的注册命令
bindings:
  command: 'myExampleCommand'
```

```yaml title=一些基础的属性
bindings:
  command:
    name: 'myExampleCommand'
    aliases:
    - example
    description: 'command description'
    permission: 'command permission'
    permissionMessage: 'no perm'
    usage: 'usage info'
```

可供使用的节点如下

| **节点**                | 接受值         | 描述   |
|-----------------------|-------------|------|
| **name**              | String      | 命令名称 |
| **aliases**           | String/List | 命令别称 |
| **description**       | String      | 命令描述 |
| **usage**             | String      | 用法提示 |
| **permission**        | String      | 命令权限 |
| **permissionMessage** | String      | 权限提示 |
| **arguments**         | List        | 参数   |

---

## 简单参数

```yaml title=示例
bindings:
  command:
    name: 'myExampleCommand'
    args:
    - 'customArg1'
    - 'customArg2'
```

- 通过此命令开启菜单，则需要提供两个参数。 
- 且两个参数自动注册到菜单语境中的变量（customArg1，customArg2）

:::tip 在菜单中使用传递的参数
使用 Kether 语句 `context` 可访问这两个自动注册的变量，即  
`context get customArg1`  
`context get customArg2`
:::

## 进阶参数

```yaml title=示例
bindings:
 command:
   name: 'sounds'
   argument:
   - label: filter
     type: ANY
     restrict: false
     optional: true
     default: value
     suggest:
     - ambient
     - block
     - enchant
     - entity
     - event
     - item
     - music
     - particle
     - ui
     - weather
```

参数对象可供使用的节点如下

| **节点**               | 接受值    | 描述                  |
|----------------------|--------|---------------------|
| **label**            | String | 参数名称                |
| **type**             | String | 参数类型                |
| **restrict**         | Bool   | 是否限制参数内容为补全的之一（默认否） |
| **optional**         | Bool   | 是否可选（默认真 ）          |
| **default**          | Any    | 参数默认值               |
| **suggest**          | List   | 自定义补全提示内容           |
| **incorrectMessage** | String | 参数出错的提示             |

- `label` 作为参数的标识符，同时也是注册到菜单语境中的变量名
- `type` 默认提供多种类型供选择，包含自动补全内容

| **类型**      | 描述     |
|-------------|--------|
| **ANY**     | 任意     |
| **DECIMAL** | 数字     |
| **INTEGER** | 整数     |
| **BOOLEAN** | 布尔值    |
| **PLAYER**  | 在线玩家名称 |
| **WORLD**   | 世界名称   |
