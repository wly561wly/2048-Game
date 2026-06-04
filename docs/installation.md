# 安装与启动指南

## 前置条件

在开始之前，请确保你的系统已安装：

- **JDK 17 或更高版本**
- **JavaFX 17 或更高版本**（JDK 17+ 不再内置 JavaFX，需单独安装）

> 如果尚未安装，请先参阅 [依赖说明](dependencies.md) 完成 JDK 和 JavaFX 的安装。

## 下载项目

### 通过 Git 克隆

```bash
git clone <repository-url>
cd 2048-Game
```

### 直接下载

下载项目压缩包并解压到本地目录。

## 使用 IntelliJ IDEA 运行（推荐）

### 1. 打开项目

1. 启动 IntelliJ IDEA
2. 选择 `File → Open`
3. 选择项目根目录（包含 `src` 文件夹的目录）

### 2. 配置 JDK

1. `File → Project Structure → Project`
2. 设置 SDK 为 JDK 17+（若未安装，点击 `Add SDK → Download JDK` 下载）
3. 设置 Language Level 为 17+

### 3. 添加 JavaFX 库

1. `File → Project Structure → Libraries`
2. 点击 `+ → Java`
3. 选择 JavaFX SDK 的 `lib` 目录
4. 点击 OK

### 4. 配置运行参数

1. `Run → Edit Configurations`
2. 选择 `Main` 类
3. 在 `VM options` 中添加：
   ```
   --module-path "JavaFX SDK路径/lib" --add-modules javafx.controls,javafx.fxml,javafx.media
   ```
   例如在 Windows 上：
   ```
   --module-path "C:\openjfx-21\lib" --add-modules javafx.controls,javafx.fxml,javafx.media
   ```

### 5. 运行

点击运行按钮或按 `Shift + F10` 启动游戏。

## 使用命令行运行

### 1. 编译

```bash
# Windows
javac --module-path "JavaFX SDK路径\lib" ^
      --add-modules javafx.controls,javafx.fxml,javafx.media ^
      -d out ^
      src\Main.java src\model\*.java src\view\*.java src\controller\*.java

# Linux / macOS
javac --module-path "JavaFX SDK路径/lib" \
      --add-modules javafx.controls,javafx.fxml,javafx.media \
      -d out \
      src/Main.java src/model/*.java src/view/*.java src/controller/*.java
```

### 2. 运行

```bash
# Windows
java --module-path "JavaFX SDK路径\lib" ^
     --add-modules javafx.controls,javafx.fxml,javafx.media ^
     -cp out Main

# Linux / macOS
java --module-path "JavaFX SDK路径/lib" \
     --add-modules javafx.controls,javafx.fxml,javafx.media \
     -cp out Main
```

## 资源文件路径说明

项目中的部分代码使用了硬编码的绝对路径引用资源文件（如图片、音乐、存档等），这些路径指向：

```
C:\Users\Taxes\IdeaProjects\cs109\resources\
```

如果你在自己的环境中运行，需要修改以下文件中的路径：

| 文件 | 需修改的路径 |
|------|-------------|
| `src/Main.java` | 图片资源路径（`mainImage`、`image`） |
| `src/view/GameScene.java` | 背景图片路径 |
| `src/view/MainScene.java` | 背景图片路径 |
| `src/model/ChessNumber.java` | 存档文件读写路径 |
| `src/model/AI_trainer.java` | AI 参数文件读写路径 |

将路径中的 `C:\Users\Taxes\IdeaProjects\cs109\resources\` 替换为你本地的 `resources` 文件夹的绝对路径。

## 常见问题

### 1. 运行时报错 "Error: JavaFX runtime components are missing"

**原因**：JavaFX 未正确配置或 VM options 未设置。

**解决**：
- 确认 JavaFX SDK 已下载并解压
- 检查 `--module-path` 参数指向正确的 JavaFX `lib` 目录
- 确认 `--add-modules` 参数包含了所需的模块

### 2. 运行时报错 "Unable to access javafx.application.Application"

**原因**：JavaFX 库未添加到项目依赖中。

**解决**：
- 在 IntelliJ IDEA 中检查 `Project Structure → Libraries` 是否包含 JavaFX
- 命令行编译时确认 `--module-path` 参数正确

### 3. 图片或资源加载失败

**原因**：资源文件路径不正确。

**解决**：
- 检查 `resources` 文件夹是否完整
- 修改代码中的硬编码路径为本地实际路径

### 4. 中文乱码

**原因**：文件编码不一致。

**解决**：
- 确保所有 Java 源文件使用 UTF-8 编码
- 在 IntelliJ IDEA 中：`Settings → Editor → File Encodings`，将所有编码设为 UTF-8
