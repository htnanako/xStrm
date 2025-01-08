# xStrm

> 本项目用于将115网盘资源创建strm文件、下载元数据到本地，快速构建emby媒体库

### 功能介绍：
- 支持将115网盘中的视频文件生成strm文件到本地
- 支持同步下载视频相关的元数据文件（如字幕、封面等）
- 支持定时任务自动同步文件
- 支持实时监控文件变化并同步(依赖CloudDrive2的webhook功能)
- 支持多任务配置，可设置不同的源目录和目标目录
- 提供Web界面，方便配置和管理

### 安装
#### DockerCli
```shell
docker run -d \
  --name xstrm \
  -p 5300:5300 \
  -v /path/to/data:/data \
  -v /path/to/media:/media \
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
      - /path/to/media:/media    # 媒体文件目录
    environment:
      - LICENSE_KEY=your_license_key  # 授权密钥
    restart: unless-stopped
```

### 配置说明
1. 环境变量：
   - `LICENSE_KEY`: 授权密钥（必需）

2. 目录说明：
   - `/data/conf`: 配置文件目录
   - `/data/logs`: 日志文件目录
   - `/media`: 媒体文件目录（可自定义）

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

### 许可说明
- 本项目需要授权码才能使用
- 授权码支持7天试用期
- 获取license_key请联系作者，或发送邮件到service@nanako.cyou提供邮箱即可

### 永久授权购买
扫描以下微信或支付宝收款码，支付¥30元(金额已设定好)，并备注邮箱，当天内处理修改用户授权信息，随后可在设置页面内查看授权信息

<img src="https://github.com/user-attachments/assets/e3d6dd1c-12da-4dff-813e-582ec3c67389" width="300px"  />
<img src="https://github.com/user-attachments/assets/c0c6dcae-0c9f-435a-b2dd-228b791665bb" width="300px"  />

