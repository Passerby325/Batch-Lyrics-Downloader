# 歌词批量下载工具 - Word 文档生成器

一款 GUI 工具，可以从 Genius/lyrics.ovh API 批量获取歌词并生成 Word 文档。

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![PyQt6](https://img.shields.io/badge/PyQt6-6.0+-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 功能特点

- ✅ 批量从网络获取歌词（Genius API + lyrics.ovh 备用）
- ✅ 自动生成 Word 文档（每首歌独立一页）
- ✅ 预览窗口检查匹配结果
- ✅ 支持从 AZLyrics 重新获取失败的歌曲
- ✅ 自动提取第一个艺术家（支持多艺术家格式）
- ✅ 首页显示未找到歌词的歌曲
- ✅ 支持浅色/深色主题切换
- ✅ 进度条显示

## 安装

### 1. 克隆或下载项目

```bash
git clone <repository-url>
cd lyrics_to_word
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
Lemon Tree - Fools Garden
Five Hundred Miles - Hedy West / The Journeymen / Peter, Paul and Mary
Scarborough Fair - Simon & Garfunkel
Hotel California - Eagles
```

**注意：**
- 使用 `-` 分隔歌名和艺术家
- 多艺术家时自动提取第一个（如 `Artist1 / Artist2` → `Artist1`）

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
   - ⚠️ 需确认（可手动勾选）
   - ❌ 错误（可点击"重新获取"尝试从其他来源获取）
6. 点击"确认并生成 Word"

### 4. 预览窗口功能

| 按钮 | 功能 |
|------|------|
| 切换主题 | 切换浅色/深色模式 |
| 全选 | 选中所有需确认的歌曲 |
| 取消全选 | 取消选中 |
| 重新获取 | 从其他来源重新获取歌词 |
| 确认并生成 | 生成 Word 文档 |

## 输出示例

```
歌词合集
━━━━━━━━━━━━━━━━━━━━━━━━━━

未找到歌词的歌曲
• Sons and Lovers - D.H.Lawrence

目录
1. Shape of You - Ed Sheeran
2. Lemon Tree - Fools Garden
...

[第1页]
Shape of You - Ed Sheeran
[歌词内容]

[第2页]
Lemon Tree - Fools Garden
[歌词内容]
...
```

## 项目结构

```
lyrics_to_word/
├── gui.py                 # GUI 主程序
├── lyrics_to_word.py     # 命令行版本
├── songs.txt             # 歌名列表（示例）
├── requirements.txt      # Python 依赖
├── output/               # 输出目录
│   └── 歌词合集.docx     # 生成的 Word 文档
└── README.md             # 说明文档
```

## 依赖库

- `lyricsgenius` - Genius API 封装
- `python-docx` - Word 文档生成
- `requests` - HTTP 请求
- `beautifulsoup4` - HTML 解析
- `PyQt6` - GUI 框架

## 配置

### Genius API Token

在 `gui.py` 中找到并替换：

```python
API_TOKEN = "your_genius_api_token_here"
```

申请地址：https://genius.com/api-clients

## 常见问题

### Q: 为什么有些歌曲找不到歌词？
A: 可能是歌曲名拼写不正确，或 Genius/lyrics.ovh 上没有该歌曲。可以在预览窗口点击"重新获取"尝试其他来源。

### Q: 遇到反爬虫限制怎么办？
A: 程序会自动切换备用数据源 lyrics.ovh。如果持续被封禁，请稍后再试。

### Q: 如何只获取指定的几首歌？
A: 在 `songs.txt` 中只保留需要的歌曲，其他删除或注释。

### Q: Word 文档如何自动生成目录？
A: 在 Word 中点击"引用" → "自动目录"即可生成目录。

## 许可证

MIT License

## 贡献

欢迎提交 Issue 和 Pull Request！