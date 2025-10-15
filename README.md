<!-- markdownlint-disable MD033 MD041 -->
<p align="center">
  <img alt="LOGO" src="https://blogxiaozheng.oss-cn-beijing.aliyuncs.com/images/logo.png" width="256" height="256" />
</p>

# 🎮 Steam Achievements Fetcher & Display

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

这是一个功能强大的工具集，用于从 Steam API 获取游戏成就数据，并提供了在 Hugo 博客中精美展示这些成就的解决方案。

这个项目既可以作为一个独立的 Python 工具来提取任何 Steam 游戏的成就信息，也可以作为一个即插即用的 Hugo 模块，让你的博客轻松拥有酷炫的成就展示墙。

效果展示：博文中查看[《魔法使之夜》全成就攻略与游玩心得](https://blogxiaozheng.site/posts/2025-10-14-%E9%AD%94%E6%B3%95%E4%BD%BF%E4%B9%8B%E5%A4%9C%E5%85%A8%E6%88%90%E5%B0%B1%E6%94%BB%E7%95%A5%E4%B8%8E%E6%B8%B8%E7%8E%A9%E5%BF%83%E5%BE%97/)

## ✨ 功能特性

-   **🐍 独立 Python 脚本**：核心功能是一个 Python 脚本，不依赖任何特定框架。
-   **🌐 多语言支持**：可同时抓取多种语言（如简体中文、英文）的成就标题和描述。
-   **📄 结构化 JSON 输出**：将成就数据保存为清晰、结构化的 JSON 文件。
-   **🤖 智能文件名**：自动根据游戏名称和 App ID 生成可读的文件名，轻松管理多个游戏的数据。
-   **🎨 Hugo 模块集成**：提供开箱即用的 Hugo Shortcodes，在文章中展示成就列表或单个成就。
-   **💅 样式优美且可定制**：内置美观的 CSS 样式，支持深色/浅色模式，并可通过 CSS 变量轻松定制。
-   **🔗 直达 Steam**：每个成就都附有直接跳转到 Steam 官方成就页面的链接。

## 🚀 快速上手

### 1. 环境准备

-   确保你已安装 Python 3。
-   克隆或下载本项目。
-   安装所需的依赖：
    ```bash
    pip install -r requirements.txt
    ```

### 2. 获取并设置 Steam API 密钥

你需要一个 Steam API 密钥来访问 Steamworks API。

1.  访问 [Steam Web API Key 页面](https://steamcommunity.com/dev/apikey) 并登录。
2.  注册一个密钥。
3.  将你的 API 密钥设置为环境变量 `STEAM_API_KEY`。

    **macOS / Linux:**
    ```bash
    export STEAM_API_KEY='你的API密钥'
    ```
    *为了方便，可将此行添加到 `.zshrc` 或 `.bashrc` 文件中。*

    **Windows (CMD):**
    ```cmd
    set STEAM_API_KEY="你的API密钥"
    ```

### 3. 运行脚本获取成就

进入 `scripts` 目录，运行 `steam_achievements.py` 脚本，并提供一个 Steam 游戏的 App ID。

```bash
cd scripts
python steam_achievements.py <APP_ID>
```

**示例：** 获取《魔法使之夜》 (App ID: 2052410) 的成就。

```bash
python steam_achievements.py 2052410
```

脚本执行成功后，会在 `data` 目录下生成一个 JSON 文件，例如 `data/steam_achievements_2052410_mahoutsukai_no_yoru.json`。

#### 命令行选项

-   `-o, --output <路径>`: 指定自定义的输出文件路径。
-   `--list-games`: 列出一些常用的游戏 App ID 作为参考。

## 📚 作为 Hugo 模块使用

你可以将此项目作为 Hugo 模块，在你的网站中轻松展示成就。

### 1. 集成到你的 Hugo 项目

将此仓库作为 Hugo Module 添加到你的项目配置中。

*（此部分将在项目发布到 GitHub 后补充具体的配置方法）*

### 2. 在文章中展示成就

我们提供了灵活的 Shortcodes 来满足不同需求。

#### 展示一个游戏的全部成就

使用 `steam_achievements_from_file` 并指定数据文件路径。

```markdown
{{</* steam_achievements_from_file file="data/steam_achievements_2052410_mahoutsukai_no_yoru.json" */>}}
```

#### 展示单个特定成就

如果你想在文章中单独提及某个成就，可以使用 `steam_achievement`。

```markdown
{{</* steam_achievement name="TROPHY_1" file="data/steam_achievements_2052410_mahoutsukai_no_yoru.json" */>}}
```
*这里的 `name` 是成就的内部 API 名称，你可以在 JSON 文件中找到它。*

## 🗂️ 多游戏管理

本工具天生支持管理多个游戏的成就数据。

1.  为每个游戏运行一次同步脚本：
    ```bash
    # 同步 魔法使之夜
    python scripts/steam_achievements.py 2052410

    # 同步 Portal
    python scripts/steam_achievements.py 400
    ```
2.  这将在 `data` 目录下创建多个独立的 JSON 文件：
    ```
    data/
    ├── steam_achievements_2052410_project.json
    └── steam_achievements_400_portal.json
    ```
3.  在文章中按需引用对应的文件即可。

## 🎨 自定义样式

成就展示组件支持深色/浅色主题，并提供了丰富的 CSS 变量供你定制。

你可以在你的网站主 CSS 文件中覆盖这些变量，以匹配你的设计风格。

```css
/* 示例：自定义颜色 */
:root {
    --steam-ach-bg-primary: #2c2c2c;
    --steam-ach-text-primary: #f0f0f0;
    --steam-ach-link-color: #79c0ff;
}
```

完整的变量列表和更详细的自定义指南，请参考 `examples/hugo/shortcodes` 目录下的 `.html` 文件。

## ⚠️ 注意事项

-   **API 密钥安全**：请妥善保管你的 Steam API 密钥，不要将其硬编码到代码或公开的仓库中。使用环境变量是最佳实践。
-   **API 使用频率**：请勿过于频繁地调用 Steam API，以免被临时限制。脚本本身不包含自动重试逻辑。
-   **Hugo 版本**：作为 Hugo 模块使用时，请确保你的 Hugo 版本不低于 `0.41`。

## 🤝 贡献

欢迎通过提交 Issue 或 Pull Request 来改进这个项目！

## 📄 许可证

此项目基于 [MIT 许可证](https://opensource.org/licenses/MIT) 开源。