# Git 操作指引

## 代理设置（国内网络环境）
本机使用 HTTP 代理 `127.0.0.1:11888` 访问 GitHub。已在全局 git config 中配置：
- `http.https://github.com.proxy=http://127.0.0.1:11888` — 仅对 GitHub 生效

## SSL 证书
由于国内网络限制，已全局关闭 SSL 证书吊销检查：
- `http.schannelCheckRevoke=false`
此设置对 GitHub 和 AWS S3（Git LFS 存储）的访问都是必要的。

## Git LFS 大文件管理
仓库中的模型文件使用 Git LFS 管理。已在 `.gitattributes` 中配置以下扩展名：
- `*.pth` — PyTorch 模型权重
- `*.pt` — PyTorch 序列化模型
- `*.onnx` — ONNX 导出模型
- `*.tflite` — TensorFlow Lite 模型
- `*.apk` — Android 安装包

### Git LFS 推送注意事项
- 大文件通过 Git LFS 自动上传到 GitHub LFS 存储（AWS S3）
- 首次推送大文件时可能会较慢（取决于网络速度）
- 如果需要单独推送 LFS 对象：`git lfs push origin main --all`
- LFS 存储有 1GB 免费配额（GitHub 免费账户）

### GitHub 认证
- 使用 Git Credential Manager for Windows 管理凭据
- 认证令牌存储在 Windows 凭据管理器中



## 首次克隆后需要执行
```bash
git lfs install  # 初始化 Git LFS
git lfs pull     # 拉取 LFS 管理的大文件
```
