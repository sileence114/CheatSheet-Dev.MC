# Fabric

## 1. 在 IDE 中调试时显示，让控制台打印 debug 级别的消息：

JVM 参数中添加 `-Dfabric.log.level=debug`

来源：Discord: [The Fabric Projtct]( https://discord.gg/v6v4pMv ) [消息链接](https://discord.com/channels/507304429255393322/507982478276034570/792194856164261958)

## 2. 添加依赖 jar

使用 `include()` 指定需要打包到 mod jar 中的依赖。

例如，我需要用到 gson 和 sankeyaml。`build.gradle` 中添加：
```groovy
dependencies {
    // ...
    // You may need to force-disable transitiveness on them.
    modImplementation "com.google.code.gson:gson:2.8.6"
    modImplementation "org.yaml:snakeyaml:1.26"
    // Needn't include gson to building.
    // include "com.google.code.gson:gson:2.8.6"
    include "org.yaml:snakeyaml:1.26"
}
```
gson 在 server.jar 里面本来就有，所以即便不 include 也能调用到 gson 的代码。

fabric-loom 会在 build 时将 include 方法指定库的生成一个 fabric mod，并打包成 jar。然后将这个jar打包至生成的 mod jar（jar-in-jar），并在 `fabric.mod.json` 中添加其路径。

jar 结构：
```
META-INF\
└─ jars\
   └─ snakeyaml-1.26.jar
pub\
assets\
```
生成的 `fabric.mod.json`：
```json
"jars": [
 {
   "file": "META-INF/jars/snakeyaml-1.26.jar"
 }
]
```

来源：Fabric Wiki: [Loader 0.4.x and You!]( https://fabricmc.net/wiki/tutorial:loader04x#nested_jars) [fabric.mod.json]( https://fabricmc.net/wiki/documentation:fabric_mod_json?s[]=jars ) 
