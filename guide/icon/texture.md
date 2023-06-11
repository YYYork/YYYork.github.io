---
sidebar_position: 2
---

# 材质

| **节点**              | 别称                   | 接受值             | 描述              |
|---------------------|----------------------|-----------------|-----------------|
| **material**        | texture, mat         | String / Object | 图标材质（原版或特殊源）    |

### 原版材质

> 高版本物品名  

```yaml
material: red stained glass pane
```

> 低版本的数字 ID - DATA

```yaml
material: '35:3'
```

:::tip 材质容错
在 Invero 的原版材质写法中，我们是忽略大小写、下划线并自动寻找相似度最高的材质的  
因此你既可以简单的写 `red stained glass pane` 也可以完整拼出 `RED_STAINED_GLASS_PANE`
:::

### 头颅材质

图标结构为根节点，头颅材质可配置如下

```yaml title=标准写法
texture:
  head: '<头颅标识符>'
```

```yaml title=简化写法
head: '<头颅标识符>'
```

这也是多态序列化的一个体现，后续其他类型的材质介绍将直接使用简化写法  
所谓头颅标识符，我们支持以下多种类型的自动判别和应用

- 自定义纹理（base64）：`eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvNDRmNDUyZDk5OGVhYmFjNDY0MmM2YjBmZTVhOGY0ZTJlNjczZWRjYWUyYTZkZmQ5ZTZhMmU4NmU3ODZlZGFjMCJ9fX0=`
- 自定义纹理（URL-hash）：`44f452d998eabac4642c6b0fe5a8f4e2e673edcae2a6dfd9e6a2e86e786edac0`
- 玩家名称：`Arasple`
- 变量：`{{player name}}`


:::info 注意
对于在线玩家，插件会获取其玩家档案实际应用的皮肤纹理  
对于离线玩家，默认请求此 ID 的正版玩家皮肤纹理  
而变量标识符的应用逻辑是，解析变量的返回值重新判断纹理类型再应用
:::

### 物品源

> 对第三方插件的支持  

| **节点**           | 别称     | 描述                   |
|------------------|--------|----------------------|
| **zaphkiel**     | zap    | Zaphkiel 插件支持        |
| **oraxen**       | -      | Oraxen 插件支持          |
| **itemsadder**   | ia     | ItemsAdder 插件支持      |
| **headdatabase** | hdb    | HeadDatabase 插件支持    |

> 序列化物品的支持

| **节点**         | 别称           | 描述                 |
|----------------|--------------|--------------------|
| **serialized** | base64, json | base64 / json 格式物品 |

> Kether 脚本物品的支持

| **节点**     | 别称  | 描述          |
|------------|-----|-------------|
| **kether** | -   | Kether 脚本物品 |

TODO_ DETAILED EXAMPLE