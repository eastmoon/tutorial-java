# 基礎操作

本範例說明 Java 程式的編譯指令。

## 開發 Java 程式

範本 [Main.java](./Main.java) 參考文獻 [Java Tutorial Example](https://www.w3schools.com/java/default.asp)。

若要執行 Java 程式，可使用 [java](https://docs.oracle.com/en/java/javase/19/docs/specs/man/java.html) 命令介面，直譯執行程式的，來確認撰寫的內容。

```
java base/Main.java
```

## 編譯 Java 程式

Java 程式完成功能，應將其內容編譯成二進內容，避免保留原始碼。

若要執行 Java 編譯，可使用 [javac](https://docs.oracle.com/en/java/javase/19/docs/specs/man/javac.html) 命令介面，將目錄下的所有 .java 檔案，編譯成 .class 檔案並放到指定的發佈目錄。

```
javac -d /cache/base ./base/*.java
```

若要測試編譯結果，則可以使用 [java](https://docs.oracle.com/en/java/javase/19/docs/specs/man/java.html) 命令指令，並指定 ```-classpath``` 到發佈目錄，與要執行的 class 名稱

```
java -classpath .:/cache/base Main
```

## 封裝 Java 編譯內容為 .jar 檔案

jar 檔案是一種 Java class 檔案的封裝包，透過此封裝可以避免散落大量的 .class 檔案在目錄中，且能指定進入點程式。

若要執行 Java 封裝，可使用 [jar](https://docs.oracle.com/en/java/javase/19/docs/specs/man/jar.html) 命令執行如下程序：

```
## 移動到編譯目錄
cd /cache/base
## 建立 manifest 檔案
echo Main-Class: Main > manifest.txt
## 封裝成 .jar 檔案
jar cfm base.jar manifest.txt *.class
```

需要注意 manifest.txt 若未提供會導致 jar 檔執行時出現 ```no main manifest attribute``` 這個未指定進入點錯誤；詳細 manifest 配置參考文獻 [Working with Manifest Files: The Basics](https://docs.oracle.com/javase/tutorial/deployment/jar/manifestindex.html)。

若要測試封裝結果，則可以使用 [java](https://docs.oracle.com/en/java/javase/19/docs/specs/man/java.html) 命令指令，需添加 ```-jar``` 指定要執行的為 jar 檔案。

```
java -jar base.jar
```
