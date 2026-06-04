# JavaFX 依赖说明

## 概述

本项目基于 JavaFX 框架开发。从 JDK 11 开始，JavaFX 已从 JDK 中移除，需要单独安装和配置。本文档将指导你完成 JDK 和 JavaFX 的安装与配置。

## JDK 安装

### 下载

推荐使用以下 JDK 发行版：

| 发行版 | 下载地址 | 说明 |
|--------|---------|------|
| Oracle JDK | https://www.oracle.com/java/technologies/downloads/ | 官方发行版 |
| OpenJDK | https://adoptium.net/ | 开源免费 |
| Liberica JDK | https://bell-sw.com/pages/downloads/ | 内含 JavaFX 的版本 |

> 推荐使用 JDK 17（LTS）或 JDK 21（LTS）。

### 安装步骤

#### Windows

1. 下载 `.msi` 或 `.exe` 安装包
2. 运行安装程序，按提示完成安装
3. 配置环境变量：
   - 新建 `JAVA_HOME`，值为 JDK 安装路径（如 `C:\Program Files\Java\jdk-17`）
   - 将 `%JAVA_HOME%\bin` 添加到 `Path` 环境变量

#### Linux

```bash
# Ubuntu / Debian
sudo apt install openjdk-17-jdk

# Fedora
sudo dnf install java-17-openjdk-devel

# 手动安装
tar -xzf openjdk-17_linux-x64_bin.tar.gz
sudo mv jdk-17 /usr/local/
```

配置环境变量：
```bash
echo 'export JAVA_HOME=/usr/local/jdk-17' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

#### macOS

```bash
# 使用 Homebrew
brew install openjdk@17

# 或下载 .dmg 安装包手动安装
```

### 验证安装

```bash
java -version
javac -version
```

输出应显示 JDK 17+ 版本信息。

## JavaFX 安装

### 方式一：下载 JavaFX SDK（推荐）

1. 访问 https://gluonhq.com/products/javafx/ 或 https://jdk.java.net/javafx21/
2. 下载对应操作系统的 JavaFX SDK 压缩包
3. 解压到本地目录，例如：
   - Windows: `C:\openjfx-21\`
   - Linux: `/opt/openjfx-21/`
   - macOS: `/usr/local/openjfx-21/`

解压后的目录结构：
```
openjfx-21/
├── legal/
├── lib/
│   ├── javafx.controls.jar
│   ├── javafx.fxml.jar
│   ├── javafx.graphics.jar
│   ├── javafx.media.jar
│   ├── javafx.swing.jar
│   ├── javafx.web.jar
│   └── ...
└── src.zip
```

### 方式二：使用 Maven

如果项目使用 Maven 构建，在 `pom.xml` 中添加依赖：

```xml
<dependencies>
    <dependency>
        <groupId>org.openjfx</groupId>
        <artifactId>javafx-controls</artifactId>
        <version>21</version>
    </dependency>
    <dependency>
        <groupId>org.openjfx</groupId>
        <artifactId>javafx-fxml</artifactId>
        <version>21</version>
    </dependency>
    <dependency>
        <groupId>org.openjfx</groupId>
        <artifactId>javafx-media</artifactId>
        <version>21</version>
    </dependency>
</dependencies>
```

### 方式三：使用 Gradle

在 `build.gradle` 中添加：

```groovy
dependencies {
    implementation 'org.openjfx:javafx-controls:21'
    implementation 'org.openjfx:javafx-fxml:21'
    implementation 'org.openjfx:javafx-media:21'
}
```

### 方式四：使用 Liberica JDK（最简单）

Liberica JDK 内置了 JavaFX，无需额外配置：

1. 访问 https://bell-sw.com/pages/downloads/
2. 下载 **Liberica JDK Full** 版本（包含 JavaFX）
3. 安装后即可直接运行 JavaFX 应用，无需额外的 `--module-path` 参数

## 本项目所需的 JavaFX 模块

本项目使用了以下 JavaFX 模块：

| 模块 | 用途 |
|------|------|
| `javafx.controls` | 按钮、标签、滑块等 UI 控件 |
| `javafx.fxml` | FXML 布局支持 |
| `javafx.media` | 背景音乐播放 |

运行时需要通过 `--add-modules` 参数指定这些模块：

```
--add-modules javafx.controls,javafx.fxml,javafx.media
```

## 配置 JavaFX

### IntelliJ IDEA 配置

1. **添加 JavaFX 库**
   - `File → Project Structure → Libraries → + → Java`
   - 选择 JavaFX SDK 的 `lib` 目录

2. **配置 VM Options**
   - `Run → Edit Configurations → Main → VM options`
   - 添加：
     ```
     --module-path "JavaFX SDK路径/lib" --add-modules javafx.controls,javafx.fxml,javafx.media
     ```

### 命令行配置

编译和运行时都需要指定 JavaFX 模块路径：

```bash
# 编译
javac --module-path "JavaFX SDK路径/lib" \
      --add-modules javafx.controls,javafx.fxml,javafx.media \
      -d out \
      src/Main.java src/model/*.java src/view/*.java src/controller/*.java

# 运行
java --module-path "JavaFX SDK路径/lib" \
     --add-modules javafx.controls,javafx.fxml,javafx.media \
     -cp out Main
```

## 常见问题

### 1. "JavaFX runtime components are missing"

这是最常见的错误，表示 JVM 找不到 JavaFX 运行时。

**解决方案**：
- 确认已下载 JavaFX SDK
- 确认 `--module-path` 指向正确的 `lib` 目录
- 确认 `--add-modules` 包含所需模块

### 2. 模块找不到（Module not found）

```
Module javafx.controls not found
```

**解决方案**：
- 检查 JavaFX SDK 版本与 JDK 版本是否匹配
- 确认 `--module-path` 路径正确且 `lib` 目录下有对应的 `.jar` 文件

### 3. 图形渲染问题

**解决方案**：
- 更新显卡驱动
- 尝试添加 VM option：`-Dprism.order=sw`（使用软件渲染）

### 4. Linux 下缺少依赖

```bash
# Ubuntu / Debian
sudo apt install libx11-dev libxext-dev libxrender-dev libxtst-dev libxi-dev libxrandr-dev

# Fedora
sudo dnf install libX11-devel libXext-devel libXrender-devel libXtst-devel libXi-devel libXrandr-devel
```
