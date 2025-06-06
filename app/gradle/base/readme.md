# 基礎操作

+ [Gradle User Manual](https://docs.gradle.org/current/userguide/userguide.html)
    - [Core Concepts](https://docs.gradle.org/current/userguide/gradle_basics.html#gradle)
    - [Part 1: Initializing the Project](https://docs.gradle.org/current/userguide/part1_gradle_init.html#part1_begin)

## Core concep

Gradle 是一套專案管理工具，其根據建置腳本中的資訊，完成自動建置、測試和佈署軟體；在其核心設計包括以下重點：

**專案 ( Projects )：**
+ Gradle 專案是可以建置的軟體，例如應用程式或程式庫。
+ 當專案為單一專案，其結構至少包含一個稱為根專案的專案。
+ 當專案為多專案，其結構包含一個根專案和任意數量的子專案。

**建置腳本 ( Build Scripts )：**
+ 建置腳本 ( Build scripts ) 向 Gradle 詳細說明了建置專案所需的步驟。
+ 每個專案可以包含一個或多個建置腳本。

建置 ( build ) 也可稱為編譯 ( compile )，端看程式語言對行為的慣用稱呼為何。

**相依關係與依賴管理 ( Dependencies and Dependency Management )：**
+ 依賴項管理是一種自動化技術，用於聲明和解析專案所需的外部資源。
+ 每個專案通常包含許多依賴函示庫，Gradle 會在建置過程中解析這些相依。

**任務 ( Tasks )：**
+ 任務是基本的工作單元，例如編譯程式碼或執行測試。
+ 每個專案在建置腳本或插件中，包含至少一個任務。

**插件 ( Plugins )：**
+ 插件用於擴充 Gradle 的功能。
+ 插件可以為專案提供多樣的任務選擇。

## 建立專案

```
## 建立並進入專案目錄
mkdir base
cd base
```

```
gradle init --type java-application  --dsl groovy
```

建立一個 Gradle 專案，用於 Java 應用程式開發，Gradle 腳本語法使用 groovy。

專案型態參考文獻 [Supported Gradle build types](https://docs.gradle.org/current/userguide/build_init_plugin.html#supported_gradle_build_types)

腳本語言可以選擇為 Groovy 或 Kotlin。

## 編譯專案

Gradle 專案會提供兩個腳本 gradlew ( for linux ) 與 gradlew.bat ( for windows )，因此編譯專案時，在不同作業系統，其指令分別如下：

+ for Linux ( or Mac )
```
./gradlew build
```
+ for Windows
```
gradlew.bat build
```

對於 Gradle 專案，控制編譯過程與配置資訊主要為以下檔案：

```
base ( aka root project )
    └ settings.gradle(.kts)
    └ app
        └ build.gradle(.kts)
```

+ 根專案 ( root project )
+ 根專案目錄下的 settings.gradle(.kts) 檔案
+ 一個或多個子專案，每個子專案目錄擁有自己的 build.gradle(.kts) 檔案

若附檔名為 .kts 表示腳本語言使用 Kotlin。

編譯完成的內容會在子專案的 build 目錄中，此目錄與 Maven 的 target 相同。
