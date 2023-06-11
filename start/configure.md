---
sidebar_position: 3
---
# 配置

若插件成功安装，你将会在服务端插件目录下看到一个名为 Invero 的目录，其结构如下

```
Invero
│  config.yml ················ 插件配置文件
│  datasource.yml ············ 数据库属性设置
│  kether.yml ················ Kether 配置文件
│  
├─data ······················· 插件本地数据
│      invero_data.db
│      
├─lang ······················· 语言文件
│      zh_CN.yml
│      
└─workspace ·················· 默认工作空间
    │  example.yml
```

### 配置文件
```yaml title=config.yml
# 工作空间
Workspaces:
  # 匹配文件名加载（正则表达式）
  filter: '^(?![#!]).*\.(?i)(conf|hocon|yaml|yml|json)$'
  # 自定义工作路径
  paths:
    - 'plugins/Invero/workspace'

# 数据库
Database:
  type: SQLITE
  sql:
    host: localhost
    port: 3306
    user: root
    password: root
    database: test
    table: invero_data

# 菜单相关配置
Menu:
  # 默认物品名称颜色
  default-name-color: "§7"
  # 默认物品描述颜色
  default-lore-color: "§7"
```