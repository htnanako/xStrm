# xStrm

![GitHub repo size](https://img.shields.io/github/repo-size/htnanako/xStrm)
![Docker Image Size (tag)](https://img.shields.io/docker/image-size/htnanako/xstrm/latest)
![Docker Pulls](https://img.shields.io/docker/pulls/htnanako/xstrm)
[![GitHub Repo stars](https://img.shields.io/github/stars/htnanako/xStrm?style=social)](https://github.com/htnanako/xStrm/stargazers)

> 本项目用于将115网盘资源创建strm文件、下载元数据到本地，快速构建emby媒体库
>
官方Telegram群组https://t.me/xstrm_chat

部署及配置可查看博客文章[xStrm不完全教程](https://blog.nanako.vip/?p=226)

### 功能介绍：
- 支持将115网盘中的视频文件生成strm文件到本地
- 支持同步下载视频相关的元数据文件（如字幕、封面等）
- 支持定时任务自动同步文件
- 支持实时监控文件变化并同步(依赖CloudDrive2的webhook功能)
- 支持多任务配置，可设置不同的源目录和目标目录
- 支持配置通知渠道，获取任务结果
- 提供Web界面，方便配置和管理
- 支持redir服务，用于转发播放请求至网盘直链
- 支持115网盘自动签到

### 安装
#### DockerCli
```shell
docker run -d \
  --name xstrm \
  -p 5300:5300 \
  -v /path/to/data:/data \
  -v /path/to/strm:/strm \
  -e LICENSE_KEY=your_license_key \
  htnanako/xstrm:latest
```

#### Docker-Compose
```yaml
services:
  xstrm:
    image: htnanako/xstrm:latest
    container_name: xstrm
    ports:
      - "5300:5300"
    volumes:
      - /path/to/data:/data  # 配置文件目录
      - /path/to/strm:/strm    # 本地strm文件目录
    environment:
      - LICENSE_KEY=your_license_key  # 授权密钥
    restart: unless-stopped
```

### 配置说明
1. 环境变量：
   - `LICENSE_KEY`: 授权密钥（必需）
   - `SERVER_URL`: 若部署在国外服务器，添加此参数并设定值为`https://x.nanako.cyou`指定验证服务器地址。若部署在国内则不需要

2. 目录说明：
   - `/data/conf`: 配置文件目录
   - `/data/logs`: 日志文件目录
   - `/strm`: 本地strm文件目录（可自定义）

3. 端口说明：
   - `5300`: Web界面和API端口

4. 实时监控
    - 需要开启CloudDrive2的webhook功能，下载webhook.toml文件，并配置其中的base_url地址为本程序地址，如`http://your-ip:5300`
    - 保存到cd2配置中的config路径下，重启cd2容器即可

### 使用说明
1. 访问 `http://your-ip:5300` 进入Web管理界面
2. 在系统设置中配置115网盘的Cookies
3. 添加同步任务，设置源目录和目标目录
4. 可选择开启定时任务或实时监控
5. 支持手动执行任务和WEB查看运行日志

### 界面预览(非最新版本，以实际为准)

![iShot_2025-01-11_13 37 23](https://github.com/user-attachments/assets/155ab4d9-4492-42af-ac00-bf262beb8db8)
![iShot_2025-01-11_13 37 31](https://github.com/user-attachments/assets/db0d44ac-ae0e-45ca-b030-05e1a4995c04)
![iShot_2025-01-11_13 37 57](https://github.com/user-attachments/assets/bbf474da-2907-46b1-818d-cbdc8c88fe3f)
![iShot_2025-01-11_13 38 53](https://github.com/user-attachments/assets/a68ac41d-175b-4466-b172-be3430829fb0)
![iShot_2025-01-11_13 39 03](https://github.com/user-attachments/assets/de1db0b9-4fa3-4612-93c5-26377d487cb6)
![iShot_2025-01-11_13 39 15](https://github.com/user-attachments/assets/49d70850-170e-41a5-9ec8-addc3ab53bbb)



### 许可说明
- 本项目需要授权码才能使用。
- 授权码支持7天试用期。
- 获取license_key请联系作者，发送邮件到 `service@nanako.cyou` 提供 `邮箱` 以及 `项目名称xStrm` ，或者试用TG群组的机器人自助申请。
- 不接受任何理由申请退款，不接受任何理由申请退款，不接受任何理由申请退款。

### 永久授权购买
永久授权价格¥68.00。软件已内置购买授权功能，申请试用码安装容器之后可在 `系统设置` -> `授权管理` 中查看授权信息和购买永久授权。目前仅支持支付宝支付。

