# QZone-Archive

在 QQ 空间彻底成为时代眼泪之前，把属于自己的互联网记忆保存下来。

作者已成功备份自 2011 年以来的 **超过10000 条动态**，包含原创内容、转发内容、评论区、楼中楼回复、长说说全文以及相册描述。

---

## 功能

- 备份 QQ 空间动态
  
- 自动补全被截断的长说说
  
- 保存转发内容（[转自]）
  
- 保存转评内容（[转评]）
  
- 保存评论区与楼中楼回复
  
- 保留 [图片]、[视频] 等媒体标记
  
- 原始接口响应存档
  
- 备份相册照片描述
  
- 支持断点续传
  
- 支持增量更新
  
- JSON 格式导出
  

---

## 环境要求

- Python 3.10+
  
- Playwright
  

安装依赖：

```bash
pip install playwright
playwright install
```

---

## 使用方法

编辑脚本中的 QQ 号：

```python
QQ = "你的QQ号"
```

运行：

```bash
python qzone_getPost_V2.py
```

首次运行需要登录 QQ 空间。

登录成功后会自动保存 Cookie。

程序会自动：

- 分页抓取动态
  
- 获取评论区
  
- 获取楼中楼回复
  
- 自动补全长说说
  
- 保存断点信息
  
- 导出 JSON 数据
  

---

## 输出文件

```text
qzone_v2_clean.json
├─ 整理后的动态数据

qzone_v2_raw.json
├─ 原始接口响应存档

checkpoint.json
└─ 断点续传信息
```

---

## 数据示例

### qzone_v2_clean.json

整理后的可读数据。

```json
{
  "time": "2023-07-08 21:34:50",
  "timestamp": 1688823290,
  "tid": "1234567890",
  "name": "ExampleUser",

  "content": "[转评] 终于把这周的事情做完了。 [转自] 总觉得时间还很多，真正开始的时候才发现已经来不及了。 [图片]",

  "comments": [
    "FriendA：太真实了",
    "ExampleUser → FriendA：下次一定"
  ],

  "has_more_con": 0,
  "detail_fetched": false
}
```

长说说补全后：

```json
{
  "time": "2024-05-01 18:20:15",
  "timestamp": 1714558815,
  "tid": "1234567891",
  "name": "ExampleUser",

  "content": "这里保存的是自动补全后的完整正文......",

  "comments": [],

  "has_more_con": 1,
  "detail_fetched": true
}
```

字段说明：

| 字段  | 说明  |
| --- | --- |
| time | 格式化时间 |
| timestamp | Unix 时间戳 |
| tid | 动态唯一 ID |
| name | 发布者昵称 |
| content | 整理后的正文 |
| comments | 评论区 |
| has_more_con | 是否为长说说 |
| detail_fetched | 是否已补全全文 |

---

### qzone_v2_raw.json

原始接口响应存档。

保留接口返回内容，便于：

- 调试
  
- 数据溯源
  
- 重新清洗
  
- 后续研究 QQ 空间接口
  

示例：

```json
{
  "tid": "228b0383ff793b6a3edf0900",

  "msglist": {
    "content": "......",
    "commentlist": [...],
    "conlist": [...],
    "has_more_con": 1,
    "created_time": 1782282751
  },

  "detail": {
    "content": "......",
    "commentlist": [...]
  }
}
```

对于普通动态：

```json
{
  "tid": "...",
  "msglist": { ... }
}
```

对于长说说：

```json
{
  "tid": "...",
  "msglist": { ... },
  "detail": { ... }
}
```

---

## 相册描述备份

运行：

```bash
python qzone_getAlbumDesc.py
```

然后：

1. 登录 QQ 空间
  
2. 打开相册
  
3. 打开任意照片
  

脚本会自动翻阅照片并保存描述。

### 输出示例

```json
{
  "旅行记录": {
    "2026-05-26": {
      "18:53": "远远看过去还以为是塑料袋，走近发现是一只猫"
    },

    "2026-05-25": {
      "21:48": "咖啡因",
      "16:48": "路过的时候顺手拍了一张"
    }
  }
}
```

输出目录：

```text
qzone_data/
├── 旅行记录.json
├── 校园日常.json
└── ...
```

---

## 涉及接口

### emotion_cgi_msglist_v6

动态列表接口。

用于获取：

- 动态正文
  
- 转发内容
  
- 评论区
  
- 时间信息
  
- 媒体信息
  

---

### emotion_cgi_msgdetail_v6

长说说详情接口。

用于补全：

```text
展开全文
长说说
被截断内容
```

获取完整正文。

---

### cgi_floatview_photo_list_v2

相册接口。

用于获取：

- 相册名称
  
- 上传时间
  
- 照片描述
  

---

## 注意事项

- QQ 空间接口可能随时发生变化。
  
- 本项目仅用于个人数据备份与归档。
  
- Cookie 仅保存在本地。
  
- 请勿用于未经授权的数据抓取。
  
- 建议定期备份导出的 JSON 文件。
  

---

## 为什么做这个项目

QQ 空间承载了许多人十几年甚至更久的互联网记忆。

随着旧平台逐渐淡出视野，很多内容未来可能不再方便访问。

这个项目的目标很简单：

> 在它们消失之前，把属于自己的互联网记忆保存下来。

---

## License

MIT

# QZone-Archive

Preserve your digital memories before QZone becomes a relic of the past.

The author has successfully archived **over 10,000 QZone posts**, including original posts, reposts, comments, nested replies, full long-post content, and photo album descriptions.

---

## Features

- Archive QZone posts
  
- Automatically recover truncated long posts
  
- Preserve reposted content (`[Repost]`)
  
- Preserve repost-with-comment content (`[Quote Repost]`)
  
- Archive comments and nested replies
  
- Preserve media markers such as `[Image]` and `[Video]`
  
- Store raw API responses for future analysis
  
- Archive photo album descriptions
  
- Checkpoint-based resume support
  
- Incremental updates
  
- JSON export
  

---

## Requirements

- Python 3.10+
  
- Playwright
  

Install dependencies:

```bash
pip install playwright
playwright install
```

---

## Usage

Edit your QQ number in the script:

```python
QQ = "YourQQNumber"
```

Run:

```bash
python qzone_getPost_V2.py
```

The first run requires logging into QZone.

After a successful login, cookies will be saved automatically.

The program will:

- Crawl posts page by page
  
- Archive comments
  
- Archive nested replies
  
- Recover full long-post content
  
- Save checkpoints
  
- Export data as JSON
  

---

## Output Files

```text
qzone_v2_clean.json
├─ Cleaned and structured post data

qzone_v2_raw.json
├─ Raw API response archive

checkpoint.json
└─ Resume checkpoint information
```

---

## Data Example

### qzone_v2_clean.json

Human-readable structured output.

```json
{
  "time": "2023-07-08 21:34:50",
  "timestamp": 1688823290,
  "tid": "1234567890",
  "name": "ExampleUser",

  "content": "[Quote Repost] Finally finished everything scheduled for this week. [Repost] Planning only takes ten minutes, actually doing it takes all day. [Image]",

  "comments": [
    "FriendA: Too real.",
    "ExampleUser → FriendA: Next time for sure."
  ],

  "has_more_con": 0,
  "detail_fetched": false
}
```

Example of a recovered long post:

```json
{
  "time": "2024-05-01 18:20:15",
  "timestamp": 1714558815,
  "tid": "1234567891",
  "name": "ExampleUser",

  "content": "This field contains the fully recovered long-post content...",

  "comments": [],

  "has_more_con": 1,
  "detail_fetched": true
}
```

Field descriptions:

| Field | Description |
| --- | --- |
| time | Formatted timestamp |
| timestamp | Unix timestamp |
| tid | Unique post ID |
| name | Author nickname |
| content | Processed post content |
| comments | Comment list |
| has_more_con | Whether the post was originally truncated |
| detail_fetched | Whether the full content was recovered |

---

### qzone_v2_raw.json

Raw API response archive.

Useful for:

- Debugging
  
- Data validation
  
- Reprocessing
  
- Reverse engineering QZone APIs
  

Example:

```json
{
  "tid": "228b0383ff793b6a3edf0900",

  "msglist": {
    "content": "...",
    "commentlist": [...],
    "conlist": [...],
    "has_more_con": 1,
    "created_time": 1782282751
  },

  "detail": {
    "content": "...",
    "commentlist": [...]
  }
}
```

For normal posts:

```json
{
  "tid": "...",
  "msglist": { ... }
}
```

For long posts:

```json
{
  "tid": "...",
  "msglist": { ... },
  "detail": { ... }
}
```

---

## Photo Album Description Backup

Run:

```bash
python qzone_getAlbumDesc.py
```

Then:

1. Log in to QZone
  
2. Open a photo album
  
3. Open any photo
  

The script will automatically browse photos and save their descriptions.

### Example Output

```json
{
  "Travel": {
    "2026-05-26": {
      "18:53": "From a distance I thought it was a plastic bag. Turned out to be a cat."
    },

    "2026-05-25": {
      "21:48": "Too much caffeine.",
      "16:48": "Took this photo while passing by."
    }
  }
}
```

Output directory:

```text
qzone_data/
├── Travel.json
├── CampusLife.json
└── ...
```

---

## APIs Used

### emotion_cgi_msglist_v6

Primary post listing API.

Used to retrieve:

- Post content
  
- Repost information
  
- Comments
  
- Timestamps
  
- Media metadata
  

---

### emotion_cgi_msgdetail_v6

Long-post detail API.

Used to recover:

```text
Expanded Content
Long Posts
Truncated Posts
```

and retrieve the complete original text.

---

### cgi_floatview_photo_list_v2

Photo album API.

Used to retrieve:

- Album names
  
- Upload timestamps
  
- Photo descriptions
  

---

## Notes

- QZone APIs may change at any time.
  
- This project is intended for personal data archiving only.
  
- Cookies are stored locally and are never uploaded anywhere.
  
- Do not use this project to collect data without authorization.
  
- Regular backups of exported JSON files are recommended.
  

---

## Why This Project Exists

For many people, QZone contains more than a decade of personal history.

As older platforms gradually fade away, accessing these memories may become increasingly difficult.

The goal of this project is simple:

> Preserve your own corner of the internet before it disappears.

---

## License

MIT
