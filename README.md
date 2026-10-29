# 网易云音乐工具箱（个人部署版）

基于开源项目 [Suxiaoqinx/Netease_url](https://github.com/Suxiaoqinx/Netease_url) 改进。原作者：**Suxiaoqinx**。原项目采用 MIT License；本仓库保留原许可证及版权声明。感谢原作者的工作。

本项目提供网易云音乐搜索、歌曲解析、歌单与专辑解析及下载功能。网易云音乐接口可能变化，歌曲可用音质和下载权限由网易云音乐账号、版权和服务端响应决定。

## 安全提醒

这是个人部署项目。上线前必须设置访问用户名和强密码，并仅通过 HTTPS 访问。不要把 `.env`、`cookie.txt`、日志或下载目录提交到 GitHub。账号 Cookie 有效时，获得网站访问权的人可能使用你的账号权限。请不要向公众开放未经保护的实例。

## 本机启动

Python 3.9 或更新版本：

```bash
python3 -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
gunicorn --bind 127.0.0.1:53187 --workers 1 --threads 4 main:app
```

访问 `http://127.0.0.1:53187`。第一次使用，在页面中扫码登录。Cookie 保存在本机 `cookie.txt`，请妥善保护。

## 公网部署

推荐部署在支持持久化磁盘和 HTTPS 的 Python Web 服务平台。启动命令：

```bash
gunicorn --bind 0.0.0.0:${PORT:-10000} --workers 1 --threads 4 main:app
```

必须配置环境变量：

- `APP_USERNAME`：访问用户名
- `APP_PASSWORD`：高强度随机密码
- `PORT`：由托管平台提供

将持久化磁盘挂载到应用目录，以保留 `cookie.txt` 和下载文件。只给可信的人分享网址和访问密码。免费实例可能休眠或不保留本地文件，需按所选平台计划确认。

## 原项目与许可

- 原项目：[Suxiaoqinx/Netease_url](https://github.com/Suxiaoqinx/Netease_url)
- 原项目作者：Suxiaoqinx
- 许可证：MIT，详见 [LICENSE](LICENSE)
- 此个人改进版不隶属于网易云音乐或原作者。
