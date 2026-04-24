# 歌词批量下载工具 - Word 文档生成器
# Batch Lyrics Downloader - Word Document Generator

一款 GUI 工具，可以从 Genius/网易云/lyrics.ovh 批量获取歌词并生成 Word 文档。

A GUI tool to batch download lyrics from Genius/NetEase/lyrics.ovh and export to Word documents.

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![PyQt6](https://img.shields.io/badge/PyQt6-6.0+-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 功能特点 / Features

- ✅ 批量从网络获取歌词（Genius API + 网易云 + lyrics.ovh）
- Batch download lyrics from multiple sources (Genius API + NetEase + lyrics.ovh)
- ✅ 自动生成 Word 文档（每首歌独立一页）
- Auto-generate Word documents (one page per song)
- ✅ 预览窗口检查匹配结果
- Preview window to check match results
- ✅ 重新搜索后需要用户确认
- Require user confirmation after retry
- ✅ 一键重试（使用网易云批量重新搜索勾选的歌曲）
- One-click retry with NetEase for selected songs
- ✅ 支持浅色/深色主题切换
- Light/Dark theme toggle
- ✅ 进度条显示下载进度
- Progress bar for download
- ✅ 首页显示未找到歌词和跳过的歌曲
- First page shows failed/skipped songs

## 安装 / Installation

### 1. 克隆或下载项目 / Clone or download

```bash
git clone https://github.com/Passerby325/Batch-Lyrics-Downloader.git
cd Batch-Lyrics-Downloader
```

### 2. 安装依赖 / Install dependencies

```bash
pip install -r requirements.txt
```

### 3. 运行 / Run

```bash
python gui.py
```

## 使用方法 / Usage

### 1. 准备歌名列表 / Prepare song list

编辑 `songs.txt` 文件，每行一首歌曲：
Edit `songs.txt`, one song per line:

```
格式 / Format：歌名 - 艺术家 / Song Name - Artist
示例 / Examples：
Shape of You - Ed Sheeran
晴天 - 周杰伦 / 晴天 - Jay Chou
Lemon Tree - Fools Garden
Hotel California - Eagles
```

注意 / Note:
- 使用 `-` 分隔歌名和艺术家 / Use `-` to separate song name and artist
- 支持中文和英文歌曲 / Supports Chinese and English songs

### 2. 操作流程 / Workflow

1. 点击"浏览..."选择 `songs.txt` 文件 / Click "Browse..." to select `songs.txt`
2. 选择输出 Word 文档的保存路径 / Choose save path for Word document
3. 点击"开始下载" / Click "Start Download"
4. 等待下载完成，弹出预览窗口 / Wait for download, preview window opens
5. 检查匹配结果 / Check match results:
   - ✅ 匹配正确 / Match correct (auto-include)
   - ⚠️ 需确认 / Needs confirmation (check and confirm)
   - 重新获取 / Retry: 从网易云重新搜索 / Retry from NetEase
   - 跳过 / Skip: 不包含在文档中 / Exclude from document
   - 确认 / Confirm: 无论勾选与否都包含 / Include regardless of checkbox
6. 可选：勾选需要重新搜索的歌曲，点击"一键重试" / Optional: Check songs to retry, click "One-click Retry"
7. 点击"生成文档"完成 / Click "Generate Document" to finish

### 3. 预览窗口功能 / Preview Window Functions

| 按钮 / Button | 功能 / Function |
|------|------|
| 切换主题 / Toggle Theme | 切换浅色/深色模式 / Switch light/dark mode |
| 全选 / Select All | 选中所有需确认的歌曲 / Check all songs needing confirmation |
| 取消全选 / Deselect All | 取消选中 / Uncheck all |
| 一键重试 / One-click Retry | 使用网易云批量重新搜索勾选的歌曲 / Batch retry selected songs via NetEase |
| 生成文档 / Generate Doc | 生成 Word 文档 / Generate Word document |

### 4. 状态说明 / Status Icons

| 图标 / Icon | 状态 / Status | 说明 / Description |
|------|------|------|
| ✅ | 匹配正确 / Match Correct | 自动包含 / Auto-include |
| ⚠️ | 需确认 / Needs Confirmation | 可勾选后确认 / Check and confirm |
| ⏳ | 待确认 / Pending | 重新获取成功，等待确认 / Retry success, waiting confirmation |
| 🔍 | 正在搜索 / Searching | 正在从网易云获取 / Fetching from NetEase |
| ❌ | 错误 / Error | 未找到歌词 / Lyrics not found |
| ⏭️ | 跳过 / Skipped | 用户跳过，不包含在文档中 / User skipped, excluded |

## 输出示例 / Output Example

```
歌词合集 / Lyrics Collection
━━━━━━━━━━━━━━━━━━━━━━━━━━

未找到歌词的歌曲 / Songs Without Lyrics
• 未找到的歌曲名 / Song not found

跳过的歌曲 / Skipped Songs
• 用户跳过的歌曲名 / User skipped song

目录 / Contents
1. Shape of You - Ed Sheeran
2. 晴天 - 周杰伦 / Jay Chou
...

[第1页 / Page 1]
Shape of You - Ed Sheeran
[歌词内容 / Lyrics content]

[第2页 / Page 2]
晴天 - 周杰伦 / Jay Chou
[歌词内容 / Lyrics content]
...
```

## 项目结构 / Project Structure

```
lyrics_to_word/
├── gui.py                 # GUI 主程序 / GUI main program
├── lyrics_to_word.py     # 命令行版本 / Command-line version
├── songs.txt             # 歌名列表 / Song list
├── requirements.txt     # Python 依赖 / Python dependencies
├── output/              # 输出目录 / Output directory
├── .gitignore          # Git 忽略配置 / Git ignore
├── CHANGELOG.md        # 更新日志 / Changelog
└── README.md           # 说明文档 / This file
```

## 依赖库 / Dependencies

- `lyricsgenius` - Genius API 封装 / Genius API wrapper
- `python-docx` - Word 文档生成 / Word document generation
- `requests` - HTTP 请求 / HTTP requests
- `beautifulsoup4` - HTML 解析 / HTML parsing
- `PyQt6` - GUI 框架 / GUI framework

## 配置 / Configuration

### Genius API Token（可选 / Optional）

在 `gui.py` 中找到并替换：
Find and replace in `gui.py`:

```python
API_TOKEN = "your_genius_api_token_here"
```

申请地址 / Apply: https://genius.com/api-clients

## 常见问题 / FAQ

### Q: 为什么有些歌曲找不到歌词？
### Q: Why some songs can't find lyrics?

A: 可能是歌曲名拼写不正确。可以点击"重新获取"尝试从其他来源获取。
A: Possible incorrect spelling. Try "Retry" to fetch from other sources.

### Q: 网易云搜索不到正确的版本？
### Q: NetEase returns wrong version?

A: 程序会自动匹配艺术家名称。如果找不到匹配的，会返回第一个结果。
A: Program tries to match artist name. If no match found, returns first result.

### Q: 如何重新搜索失败的歌曲？
### Q: How to retry failed songs?

A: 在预览窗口勾选需要重新搜索的歌曲，点击"一键重试"。
A: Check songs to retry in preview window, click "One-click Retry".

### Q: 确认按钮的作用是什么？
### Q: What does the Confirm button do?

A: 无论是否勾选，点击确认后歌曲都会被包含在 Word 文档中。
A: Song will be included in Word document regardless of checkbox state.

## 许可证 / License

MIT License

## 贡献 / Contributing

欢迎提交 Issue 和 Pull Request！
Issues and Pull Requests are welcome!