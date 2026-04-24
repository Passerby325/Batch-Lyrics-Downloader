# 歌词批量下载工具 - Word 文档生成器

一款 GUI 工具，可以从 Genius/网易云/lyrics.ovh 批量获取歌词并生成 Word 文档。

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![PyQt6](https://img.shields.io/badge/PyQt6-6.0+-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 功能特点

- ✅ 批量从网络获取歌词（Genius API + 网易云 + lyrics.ovh）
- ✅ 自动生成 Word 文档（每首歌独立一页）
- ✅ 预览窗口检查匹配结果
- ✅ 重新搜索后需要用户确认
- ✅ 一键重试（使用网易云批量重新搜索勾选的歌曲）
- ✅ 支持浅色/深色主题切换
- ✅ 进度条显示下载进度
- ✅ 首页显示未找到歌词和跳过的歌曲

## 安装

### 1. 克隆或下载项目

```bash
git clone https://github.com/Passerby325/Batch-Lyrics-Downloader.git
cd Batch-Lyrics-Downloader
```

### 2. 安装依赖

```bash
pip install -r requirements.txt
```

### 3. 运行

```bash
python gui.py
```

## 使用方法

### 1. 准备歌名列表

编辑 `songs.txt` 文件，每行一首歌曲：

```
格式：歌名 - 艺术家
示例：
Shape of You - Ed Sheeran
晴天 - 周杰伦
Lemon Tree - Fools Garden
```

**注意：**
- 使用 `-` 分隔歌名和艺术家
- 支持中文和英文歌曲

### 2. 运行程序

```bash
python gui.py
```

### 3. 操作流程

1. 点击"浏览..."选择 `songs.txt` 文件
2. 选择输出 Word 文档的保存路径
3. 点击"开始下载"
4. 等待下载完成，弹出预览窗口
5. 检查匹配结果：
   - ✅ 匹配正确（自动包含）
   - ⚠️ 需确认（可手动勾选后点击确认）
   - 重新获取：从网易云重新搜索
   - 跳过：不包含在文档中
   - 确认：无论勾选与否都包含
6. 可选：勾选需要重新搜索的歌曲，点击"一键重试"
7. 点击"生成文档"完成

### 4. 预览窗口功能

| 按钮 | 功能 |
|------|------|
| 切换主题 | 切换浅色/深色模式 |
| 全选 | 选中所有需确认的歌曲 |
| 取消全选 | 取消选中 |
| 一键重试 | 使用网易云批量重新搜索勾选的歌曲 |
| 生成文档 | 生成 Word 文档 |

### 5. 状态说明

| 图标 | 状态 | 说明 |
|------|------|------|
| ✅ | 匹配正确 | 自动包含 |
| ⚠️ | 需确认 | 可勾选后确认 |
| ⏳ | 待确认 | 重新获取成功，等待确认 |
| 🔍 | 正在搜索 | 正在从网易云获取 |
| ❌ | 错误 | 未找到歌词 |
| ⏭️ | 跳过 | 用户跳过，不包含在文档中 |

## 输出示例

```
歌词合集
━━━━━━━━━━━━━━━━━━━━━━━━━━

未找到歌词的歌曲
• 未找到的歌曲名

跳过的歌曲
• 用户跳过的歌曲名

目录
1. Shape of You - Ed Sheeran
2. 晴天 - 周杰伦
...

[第1页]
Shape of You - Ed Sheeran
[歌词内容]

[第2页]
晴天 - 周杰伦
[歌词内容]
...
```

## 项目结构

```
lyrics_to_word/
├── gui.py                 # GUI 主程序
├── lyrics_to_word.py     # 命令行版本
├── songs.txt             # 歌名列表
├── requirements.txt     # Python 依赖
├── output/              # 输出目录
│   ├── app.log          # 日志文件
│   └── 歌词合集.docx    # 生成的 Word 文档
├── .gitignore          # Git 忽略配置
├── CHANGELOG.md        # 更新日志
└── README.md           # 说明文档
```

## 依赖库

- `lyricsgenius` - Genius API 封装
- `python-docx` - Word 文档生成
- `requests` - HTTP 请求
- `beautifulsoup4` - HTML 解析
- `PyQt6` - GUI 框架

## 配置

### Genius API Token（可选）

在 `gui.py` 中找到并替换：

```python
API_TOKEN = "your_genius_api_token_here"
```

申请地址：https://genius.com/api-clients

## 常见问题

### Q: 为什么有些歌曲找不到歌词？
A: 可能是歌曲名拼写不正确。可以点击"重新获取"尝试从其他来源获取。

### Q: 网易云搜索不到正确的版本？
A: 程序会自动匹配艺术家名称。如果找不到匹配的，会返回第一个结果。

### Q: 如何重新搜索失败的歌曲？
A: 在预览窗口勾选需要重新搜索的歌曲，点击"一键重试"。

### Q: 确认按钮的作用是什么？
A: 无论是否勾选，点击确认后歌曲都会被包含在 Word 文档中。

## 许可证

MIT License

## 贡献

欢迎提交 Issue 和 Pull Request！