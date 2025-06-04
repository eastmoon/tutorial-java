# Java

Tutorial and training source code about Java.

## 專案操作

+ 啟動

使用 CLI 呼叫 docker-compose 來啟動相關服務

```
dev [java | maven | gradle]
```

依據選擇的項目會啟動不同的容器環境：

+ ```dev java``` 會啟動僅有 OpenJDK 的環境
+ ```dev maven``` 會啟用有 OpenJDK 與開發工具 Maven 的環境
+ ```dev gradle``` 會啟用有 OpenJDK 與開發工具 Gradle 的環境


## 文獻

+ 環境
    - [openjdk - Docker](https://hub.docker.com/_/openjdk)
    - [Apache Maven - Docker](https://hub.docker.com/_/maven)
    - [Gradle - Docker](https://hub.docker.com/_/gradle)
+ 教學
    - [Java - w3schools](https://www.w3schools.com/java/)
+ Java project management tools
    - [Apache Maven](https://maven.apache.org/)
    - [Gradle](https://gradle.org/)
