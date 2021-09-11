# 二级认证

在某些敏感操作下，我们需要对已登录的会话进行二次验证

比如 Gitee 的仓库删除操作，虽然我们已经登录了账号，当我们点击 **[删除]** 按钮时，还是需要再次输入一遍密码，这么做主要为了两点：

1. 保证操作者是当前账号本人
2. 增加操作步骤，防止误删除重要数据

这就是我们本篇要讲的 —— 二级认证，即：在已登录会话的基础上，进行再次验证，提高会话的安全性。


--- 

## 具体API

在`Sa-Token`中进行二级认证非常简单，只需要使用以下API：

``` java
// 在当前会话 开启二级认证，时间为120秒
StpUtil.openSafe(120); 

// 获取：当前会话是否处于二级认证时间内
StpUtil.isSafe(); 

// 检查当前会话是否已通过二级认证，如未通过则抛出异常
StpUtil.checkSafe(); 

// 获取当前会话的二级认证剩余有效时间 (单位: 秒, 返回-2代表尚未通过二级认证)
StpUtil.getSafeTime(); 

// 在当前会话 结束二级认证
StpUtil.closeSafe(); 
```


## 使用注解进行二级认证
在一个方法上使用 `@SaCheckSafe` 注解，可以在代码进入之前此方法之前进行一次二级认证
``` java
// 二级认证：必须二级认证之后才能进入该方法 
@SaCheckSafe      
@RequestMapping("add")
public String add() {
    return "用户增加";
}
```

详细使用方法可参考：[注解鉴权](/use/at-check)，此处不再赘述

