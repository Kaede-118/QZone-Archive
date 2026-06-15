# QZone Archive

在 QQ 空间彻底成为时代眼泪之前，把属于自己的互联网记忆保存下来。

## 功能

* 备份 QQ 空间说说
* 备份相册描述
* 支持断点续传
* 支持增量更新
* JSON 格式导出

## 环境要求

* Python 3.10+
* Playwright

安装依赖：

```bash
pip install playwright
playwright install
```

## 使用方法

### 备份说说

编辑 `qzone_getPost.py`：

```python
QQ = "你的QQ号"
```

运行：

```bash
python qzone_getPost.py
```

首次运行需要登录 QQ 空间，登录成功后会自动保存 Cookie。

程序会自动：

* 分页抓取说说
* 保存评论
* 保存转发内容
* 保存断点
* 导出 JSON

输出文件：

```text
qzone_v6_backup.json
```

---

### 备份相册描述

运行：

```bash
python qzone_getAlbumDesc.py
```

然后：

1. 登录 QQ 空间
2. 打开相册
3. 打开任意一张照片

脚本会自动翻阅照片并保存描述。

输出目录：

```text
qzone_data/
├── 相册A.json
├── 相册B.json
└── ...
```

## 注意事项

* QQ 空间接口可能随时发生变化。
* 本项目仅用于个人数据备份与归档。
* Cookie 仅保存在本地，不会上传到任何服务器。
* 请勿用于未经授权的数据抓取。

---

# English

Archive your QQ Zone memories before they disappear forever.

## Features

* Backup QQ Zone posts
* Backup album descriptions
* Incremental updates
* Resume from checkpoints
* JSON export

## Requirements

* Python 3.10+
* Playwright

Install dependencies:

```bash
pip install playwright
playwright install
```

## Usage

### Backup Posts

Edit `qzone_getPost.py`:

```python
QQ = "Your QQ Number"
```

Run:

```bash
python qzone_getPost.py
```

The script will:

* Save login cookies locally
* Fetch posts page by page
* Save reposts and comments
* Resume from checkpoints
* Export all data as JSON

Output:

```text
qzone_v6_backup.json
```

---

### Backup Album Descriptions

Run:

```bash
python qzone_getAlbumDesc.py
```

Then:

1. Log in to QQ Zone
2. Open Albums
3. Open the first photo

The script will automatically browse photos and save descriptions.

Output:

```text
qzone_data/
├── AlbumA.json
├── AlbumB.json
└── ...
```

## Notes

* QQ Zone APIs may change at any time.
* This project is intended for personal data backup and archival purposes only.
* Cookies are stored locally and are never uploaded anywhere.
* Please do not use this project for unauthorized data collection.

## License

MIT
