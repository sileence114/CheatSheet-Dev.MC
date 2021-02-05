# Fabric

## 1. 在 IDE 中调试时显示，让控制台打印 debug 级别的消息：

JVM 参数中添加 `-Dfabric.log.level=debug`

来源：Discord: [The Fabric Projtct]( https://discord.gg/v6v4pMv ) [消息链接](https://discord.com/channels/507304429255393322/507982478276034570/792194856164261958)

## 2. 添加依赖jar

在 `fabric.mod.json` 中添加：
```
"jars": [
   {
      "file": "nested/vendor/dependency.jar"
   }
]
```

来源：Fabric Wiki: [fabric.mod.json]( https://fabricmc.net/wiki/documentation:fabric_mod_json?s[]=jars )
