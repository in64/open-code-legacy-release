# OpenCode Legacy GLIBC Build

这是一个用于构建 OpenCode 兼容老版本 GLIBC 系统的 GitHub Actions 项目。

## 背景

OpenCode 官方的预编译二进制文件依赖较新版本的 GLIBC (2.32+)，这导致在某些老系统（如 QNAP NAS、某些旧版 Linux 发行版）上无法运行。本项目通过将 OpenCode 链接到 musl libc 来解决兼容性问题。

## 工作原理

1. 每天自动检查上游 [anomalyco/opencode](https://github.com/anomalyco/opencode) 仓库的新版本
2. 使用 Docker 构建兼容版本：
   - 基于 `oven/bun:1.3.5-debian` 构建 OpenCode
   - 使用 `patchelf` 修改二进制文件的动态链接器路径
   - 从 Alpine 打包 musl 库和相关依赖
3. 自动创建 GitHub Release 并上传构建产物

## 使用方法

### 使用 mise 安装

```bash
mise install github:pedropombeiro/opencode@v1.1.35-legacy-glibc
```

### 手动安装

1. 从 [Releases](https://github.com/in64/open-code-legacy-release/releases) 下载对应版本的 tar.gz 文件
2. 解压到任意目录
3. 运行 `./bin/opencode`

## 自动构建

- **触发方式**：每天 UTC 6:00 自动检查上游新版本
- **手动触发**：通过 GitHub Actions 手动指定版本号构建

## 项目结构

```
.
├── .github/workflows/
│   └── build-legacy-glibc.yml  # GitHub Actions 工作流
└── build/legacy-glibc/
    └── Dockerfile               # Docker 构建文件
```

## 许可证

继承自上游 [anomalyco/opencode](https://github.com/anomalyco/opencode)。
