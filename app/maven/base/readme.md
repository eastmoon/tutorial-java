# 基礎操作

+ [Maven Getting Started Guide](https://maven.apache.org/guides/getting-started/index.html)
    - [Running Apache Maven](https://maven.apache.org/run.html)
    - [Introduction to the Build Lifecycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)
    - [Introduction to the POM](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html)
+ 文獻
    - [20+ Maven Commands and Options (Cheat Sheet)](https://www.digitalocean.com/community/tutorials/maven-commands-options-cheat-sheet)
    - [Maven: The Complete Reference - 6.1. Maven Command Line Options](https://books.sonatype.com/mvnref-book/reference/running-sect-options.html)

Maven 是一套 Java 專案管理工具，透過命令 ```mvn``` 建立、編譯、測試、管理專案。

本範例則是基於 Maven 的基礎操作與說明，詳細的操作指令說明與配置設定方式參考上述連結。

## 建立專案

Maven 建立專案使用參數 [archetype:generaate](https://maven.apache.org/guides/mini/guide-creating-archetypes.html)，並以下列命令句建立專案：

```
## 建立 base 專案
mvn archetype:generate \
  -DgroupId=app \
  -DartifactId=base \
  -Dversion=1.0.0 \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DarchetypeVersion=1.5 \
  -DinteractiveMode=false
```

+ groupId：專案的群組名稱
+ artifactId：專案名稱
+ version：專案版本
+ archetypeArtifactId：Archetype 的項目名稱
    - 項目列表可參考 [Maven Archetypes](https://maven.apache.org/archetypes/index.html)
+ archetypeVersion：Archetype 的版本編號
    - 版本編號可以從 Archetype 項目列表中各項目內參考，主要用於指定專案框架版本
+ interactiveMode：專案建立的互動模式開啟或關閉

## Maven 操作

以下操作皆需進入專案目錄：

+ ```mvn test```：測試專案
+ ```mvn compile```：編譯專案，預設輸出至 target 目錄下
+ ```mvn package```：將編譯內容封裝至 .jar 檔案，預設輸出至 target 目錄下
+ ```mvn site```：產生專案文件網頁
+ ```mvn clean```：移除 target 目錄

需注意，上述操作需要的詳細設定是基於專案中的 [pom](pom.xml) 檔案設定，此檔案也是 Maven 最主要的專案管理配置檔。

## 編譯後執行

在執行完 ```mvn compile``` 後，若要驗證內容，可利用 [java](https://docs.oracle.com/en/java/javase/19/docs/specs/man/java.html) 命令指令，並指定 ```-classpath``` 到發佈目錄，與要執行的 class 名稱

```
java -classpath .:${PWD}/target/classes [package].[class]
```

以當前範本為例，則實際句型如下：

```
java -classpath .:${PWD}/target/classes app.App
```

此外，也可使用 Maven 插件 exec-maven-plugin 來執行，詳細可參考 [Run a Java Main Method in Maven](https://www.baeldung.com/maven-java-main-method)

## 封裝後執行

在執行完 ```mvn compile``` 後，若要對 .class 檔案封裝為 .jar 檔案，則需執行 ```mvn package```，此操作會受到 pom.xml 中 maven-jar-plugin 的配置影響。

倘若未經過設定，封裝的 jar 檔案會出現 ```no main manifest attribute``` 錯誤，相關議題可參考文獻 [Fixing the Missing Main-Class Attribute in Maven JAR Files](https://udayangana98.medium.com/22c5c21b6878)；其主要是在增加以下設定，來補充 manifest 的內容

```xml
<project>
    <build>
        <pluginManagement>
            <plugins>
                <plugin>
                    <artifactId>maven-jar-plugin</artifactId>
                    <version>3.4.2</version>
                    <configuration>
                        <archive>
                            <manifest>
                                <mainClass>${project.groupId}.Main</mainClass>
                            </manifest>
                        </archive>
                    </configuration>
                </plugin>
            </plugins>
        </pluginManagement>
    </build>
</project>
```
> pom.xml 內容

倘若為確保設定不任意變更，建議入口類別都採用 Main.java 命名。
