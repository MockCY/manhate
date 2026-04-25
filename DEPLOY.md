# 自动化部署说明

这个项目是纯静态官网，推荐部署到 Linux 服务器的 Nginx 目录，并用 GitHub Actions 自动同步文件。

## 1. 服务器准备

登录服务器后安装 Nginx：

```bash
sudo apt update
sudo apt install -y nginx
```

创建网站目录：

```bash
sudo mkdir -p /var/www/mahate
sudo chown -R $USER:$USER /var/www/mahate
```

配置 Nginx：

```bash
sudo nano /etc/nginx/sites-available/mahate
```

写入：

```nginx
server {
    listen 80;
    server_name your-domain.com www.your-domain.com;

    root /var/www/mahate;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

启用站点：

```bash
sudo ln -s /etc/nginx/sites-available/mahate /etc/nginx/sites-enabled/mahate
sudo nginx -t
sudo systemctl reload nginx
```

## 2. 创建部署 SSH Key

在本机生成一把专门给 GitHub Actions 用的 key：

```bash
ssh-keygen -t ed25519 -C "github-actions-deploy" -f ./github-actions-deploy
```

把公钥放到服务器：

```bash
ssh-copy-id -i ./github-actions-deploy.pub 用户名@服务器IP
```

私钥内容稍后放到 GitHub Secrets：

```bash
cat ./github-actions-deploy
```

## 3. GitHub 仓库 Secrets

进入 GitHub 仓库：

`Settings` -> `Secrets and variables` -> `Actions` -> `New repository secret`

添加：

| 名称 | 示例 |
| --- | --- |
| `SSH_PRIVATE_KEY` | `github-actions-deploy` 私钥完整内容 |
| `REMOTE_HOST` | `1.2.3.4` |
| `REMOTE_USER` | `ubuntu` |
| `REMOTE_PORT` | `22` |
| `REMOTE_TARGET` | `/var/www/mahate` |

## 4. 推送代码

```bash
git init
git add .
git commit -m "Initial website"
git branch -M main
git remote add origin https://github.com/你的用户名/你的仓库名.git
git push -u origin main
```

以后每次改完代码并推送到 `main`，GitHub Actions 会自动部署到服务器。

## 5. 域名 HTTPS

域名解析到服务器 IP 后，安装 HTTPS：

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com -d www.your-domain.com
```
