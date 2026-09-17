# K7 LazyCat App

[K7](https://github.com/kaybi-gh/K7) 自托管家庭影音媒体服务器（电影、剧集、音乐），懒猫桌面应用版（LPK v2）。

## 功能

- K7 媒体服务器（Web UI + 转码 + 元数据 + 联邦）
- PostgreSQL 18 数据库（密码自动生成，免配置）
- 媒体目录挂载：懒猫媒体库 `/lzcapp/run/mnt/media` → 容器 `/media`（只读）
- 数据持久化：配置 / 元数据 / 日志 / 转码缓存 → `/lzcapp/var/k7`
- HTTPS 安全 Cookie（LazyCat 网关 TLS 终止）与 BaseUrl 自动注入（OIDC / 联邦可用）

## 使用

1. 从应用入口打开 K7，完成首次设置（创建管理员账号）
2. 在管理后台创建媒体库，指向 `/media` 下的目录（如 `/media/movies`）
3. 开始观影

## 镜像模式

- `k7-server`: 镜像 `ghcr.io/kaybi-gh/k7`，通过 `ghcr.1ms.run` 加速器拉取（mirror 模式，digest 校验）
- `postgres`: `docker.1ms.run/postgres:18-alpine`（固定依赖）

## 构建

```bash
lzc-cli project release -o dist/k7.lpk
```

## 发布

GitHub Actions（`.github/workflows/lazycat.yml`）定时 + 手动触发：

1. 检查上游最新版本
2. 更新 manifest 镜像与版本号
3. 构建 LPK 并创建 GitHub Release（版本化 asset）
4. 发布到喵喵商店（私有商店）

所需 Secrets（仓库或组织级）：

- `APPSTORE_URL` / `APPSTORE_TOKEN`（喵喵商店）
- `APP_ID`（可选）
- `PRIVATE_STORE_GROUP_CODES`（可选，分组码）

## 许可

AGPL-3.0（上游 K7 许可）
