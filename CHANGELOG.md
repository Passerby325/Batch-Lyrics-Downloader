# 修改日志 (Changelog)

本文档记录项目的所有重要修改，便于 AI 和程序员理解代码演进。

---

## [2025-04-25] v1.4.0 - 网易云音乐集成

### 新增功能
- 网易云音乐 API 集成获取歌词
- 预览窗口添加"网易云"按钮（粉红色 #e91e63）
- 新增 `fetch_lyrics_from_netease()` 函数

### 技术细节
- 网易云搜索 API: `http://music.163.com/api/search/get/`
- 网易云歌词 API: `http://music.163.com/api/song/lyric?id={id}&lv=-1&tv=-1`
- 参数 lv=-1 才能获取完整歌词（有些歌曲需要）
- 优先匹配中文歌曲（华语歌词库丰富）

### 按钮说明
| 按钮 | 功能 | 颜色 |
|------|------|------|
| 重新获取 | 先尝试 lyrics.ovh/AZLyrics，再尝试网易云 | 橙色 #ff9800 |
| 网易云 | 直接从网易云获取 | 粉色 #e91e63 |
| 跳过 | 跳过这首歌 | 灰色 #9e9e9e |

---

## [2025-xx-xx] v1.3.0 - 文档优化

### 新增功能
- 基础 GUI 界面 (PyQt6)
- Genius API 集成获取歌词
- Word 文档生成（每首歌独立一页）
- 预览窗口显示匹配结果

---

## [2025-xx-xx] v1.1.0 - 预览功能增强

### 新增功能
- 预览窗口添加匹配检查功能
- 显示状态：✅ 匹配正确 / ⚠️ 需确认 / ❌ 错误
- 全选/取消全选按钮
- 切换主题（浅色/深色）

### 修改
- 优化匹配算法，支持模糊匹配
- 统一 `&` ↔ `and`、`ft.` ↔ `feat.` 等
- 移除版本标注如 `(Dialogue Mix)`

---

## [2025-xx-xx] v1.2.0 - AZLyrics 集成

### 新增功能
- 从 AZLyrics/lyrics.ovh 重新获取歌词功能
- 预览窗口添加"重新获取"按钮
- 简化预览窗口布局（不显示歌词内容）
- 预览窗口默认隐藏 ✅ 匹配的歌曲

### 问题修复
- 修复 AZLyrics 反爬虫限制
- 使用 lyrics.ovh API 作为主要备选源

---

## [2025-xx-xx] v1.3.0 - 文档优化

### 新增功能
- Word 首页显示"未找到歌词的歌曲"
- Word 首页显示"未选中的歌曲"（分开显示）
- 解析优化：支持多艺术家格式（Artist1 / Artist2 → Artist1）

---

## 代码结构说明

### 主文件
- `gui.py` - GUI 主程序（所有功能集成）
- `lyrics_to_word.py` - 命令行版本（已较少使用）

### 核心类
1. `LyricsDownloaderThread` - 歌词下载线程
2. `PreviewDialog` - 预览确认窗口
3. `LyricsGUI` - 主窗口

### 核心函数
- `fetch_lyrics_from_azlyrics()` - 从 lyrics.ovh/AZLyrics 获取歌词
- `parse_songs_file()` - 解析 songs.txt
- `normalize_text()` - 文本标准化
- `fuzzy_match()` - 模糊匹配
- `check_match()` - 检查匹配结果
- `generate_word()` - 生成 Word 文档

---

## 待完成功能

- [ ] KKBOX 歌词集成（网页抓取方案）
- [ ] 进度条优化显示
- [ ] 批量重试功能
- [ ] 歌词翻译功能

---

## 依赖库

```
lyricsgenius>=3.0.0
python-docx>=0.8.11
requests>=2.25.1
PyQt6>=6.0.0
beautifulsoup4>=4.9.0
```

---

## 配置

### Genius API Token
在 `gui.py` 中：
```python
API_TOKEN = "your_token_here"
```

申请地址：https://genius.com/api-clients

---

## 常见问题

### Q: 预览窗口显示的歌曲太少？
A: ✅ 匹配的歌曲默认不显示，只有 ⚠️ 和 ❌ 的才显示

### Q: 为什么有些歌找不到歌词？
A: Genius/lyrics.ovh 上可能没有该歌曲，可尝试"重新获取"

### Q: 如何修改歌名列表？
A: 编辑 `songs.txt`，格式：`歌名 - 艺术家`

---

## 贡献者

- 初始开发：AI Assistant

---

## 许可证

MIT License