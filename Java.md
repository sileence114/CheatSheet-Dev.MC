# Java

1. 获取资源文件

```java
InputStream stream;
stream = this.getClass().getClassLoader().getResourceAsStream("file.json");
stream = ClassName.class.getClassLoader().getResourceAsStream("file.json");// 静态方法
URL url;
url = this.getClass().getClassLoader().getResource("file.json");
url = ClassName.class.getClassLoader().getResource("file.json");// 静态方法
```

2. 依赖
使用Gradle将项目打包为 `.jar` 文件后，Jar 中只含有本项目的class，不含有依赖。

在测试环境中能正常运行，而打包后安装至mods或plugins文件夹后会报 `ClassNotFoundException` 异常。

解决方式有两种：**class path** 和 **shadow**
* class-path

例如 Mohist 的文件夹结构：
```
...
libraries/
  | .../
  | org/
     | yaml/
        | snakeyaml/
           | 1.19/
              | snakeyaml-1.19.jar
mohist-1.12.2-180-server.jar
eula.txt
```
Mohist 和 CatServer 端在第一次加载时就会创建一个lib文件夹，__然后占用主线程__联网下载 jar 文件，再添加到 class path。

当然某些不是很规范的 Bukkit 插件也会干这种事。__点名 TrChat。__

Fabric MOD 在 build.gradle 选择将依赖 jar 一起打包到 META-INF/jars，然后在 fabric.mod.json 中指定其名路径，fabric 在加载 MOD 时会将其添加到 class-path。[详情]()

* [shadow]( https://imperceptiblethoughts.com/shadow/introduction/ )

例如server.jar就是这样的：（server.jar 的结构）
```
assets/...
net/
  | data/...
  | world/...
  | server/...
com/
  | google/
    | ...
    | gson
      | ....class
```
将依赖中的类直接打包放到项目的jar中。项目的类可以直接通过包名访问。