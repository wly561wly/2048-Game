# 2048 妙妙屋

基于 JavaFX 开发的 2048 桌面游戏，支持经典模式、挑战模式、无尽模式以及 AI 自动游玩。

## 功能特性

- **经典模式** — 选择目标方块（512 / 1024 / 2048 / 4096），合成目标即获胜
- **挑战模式** — 限时挑战（30s / 60s / 90s / 120s），在规定时间内尽可能拿高分
- **无尽模式** — 无目标、无时间限制，追求最高分数
- **AI 模式** — 观看 AI 自动对局
- **用户系统** — 注册 / 登录 / 游客登录，支持密码找回
- **存档系统** — 手动保存 / 加载存档，支持自动保存
- **排行榜** — 各模式独立排名
- **撤销** — 支持撤销上一步操作
- **提示** — 提供下一步建议
- **主题切换** — 5 种颜色主题（Classic / Green & Blue / Pink / Blue / Yellow & Red）
- **棋盘大小** — 支持 3×3 到 10×10 的棋盘

## 快速开始

### 环境要求

| 依赖 | 版本要求 |
|------|---------|
| JDK | 17+ |
| JavaFX | 17+ |

### 下载

```bash
git clone <repository-url>
cd 2048-Game
```

### 编译与运行

#### 方式一：IntelliJ IDEA（推荐）

1. 用 IntelliJ IDEA 打开项目根目录
2. 确保项目 SDK 设置为 JDK 17+
3. 添加 JavaFX 库：`File → Project Structure → Libraries → + → JavaFX SDK 路径`
4. 配置 VM Options：
   ```
   --module-path "JavaFX SDK路径/lib" --add-modules javafx.controls,javafx.fxml,javafx.media
   ```
5. 运行 `src/Main.java`

#### 方式二：命令行

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

> 详细的环境配置与 JavaFX 安装指南请参阅 [依赖说明](docs/dependencies.md)

## 项目结构

```
2048-Game/
├── src/
│   ├── Main.java                 # 程序入口，场景切换与事件绑定
│   ├── controller/
│   │   └── GameController.java   # 游戏控制器
│   ├── model/
│   │   ├── ChessNumber.java      # 棋盘数据模型（移动、合并、存档）
│   │   ├── AI_trainer.java       # AI 训练器
│   │   ├── Assess.java           # AI 评估函数
│   │   ├── RankElement.java      # 排行榜元素
│   │   └── UserImform.java       # 用户信息模型
│   └── view/
│       ├── StartScene.java       # 启动界面
│       ├── LoginScene.java       # 登录界面
│       ├── RegisterScene.java    # 注册界面
│       ├── ForgetScene.java      # 忘记密码界面
│       ├── MainScene.java        # 主菜单界面
│       ├── ClassicChooseScene.java  # 经典模式选择
│       ├── ChallengeChooseScene.java# 挑战模式选择
│       ├── GameScene.java        # 游戏主界面
│       ├── AIscene.java          # AI 对局界面
│       ├── ChessPane.java        # 棋盘渲染
│       ├── GameOver.java         # 游戏结束弹窗
│       ├── Help.java             # 帮助界面
│       ├── MenuBar.java          # 菜单栏
│       ├── RankList.java         # 排行榜
│       ├── Setting.java          # 设置界面
│       └── ListenPanel.java      # 监听面板
├── resources/
│   ├── image/                    # 图片资源
│   ├── music/                    # 音乐资源
│   ├── rank/                     # 排行榜数据
│   └── users/                    # 用户存档数据
└── docs/                         # 文档
    ├── gameplay.md               # 游戏玩法详解
    ├── installation.md           # 安装与启动指南
    └── dependencies.md           # JavaFX 依赖说明
```

## 文档

| 文档 | 说明 |
|------|------|
| [如何游玩](docs/gameplay.md) | 游戏规则、操作方式、各模式详解 |
| [安装与启动](docs/installation.md) | 下载、编译、运行的完整步骤 |
| [依赖说明](docs/dependencies.md) | JDK 与 JavaFX 的安装配置 |

## 操作方式

| 操作 | 按键 |
|------|------|
| 上移 | `↑` 或 `W` |
| 下移 | `↓` 或 `S` |
| 左移 | `←` 或 `A` |
| 右移 | `→` 或 `D` |

也可以使用界面上的方向按钮进行操作。

## 许可证

本项目仅供学习交流使用。
