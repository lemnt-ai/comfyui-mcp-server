# ComfyUI MCP Server

基于 FastMCP 的 ComfyUI 服务，提供 AI 视频生成相关功能的 MCP（Model Context Protocol）接口。

## 功能

- **视频生成** - 调用 ComfyUI 生成视频
- **分镜生成** - 生成分镜脚本
- **视频合成** - 合成多个视频片段
- **进度检查** - 检查任务执行进度
- **视频下载** - 下载生成的视频

## 安装

```bash
# 克隆项目
git clone <repository-url>
cd comfyui-mcp-server

# 创建虚拟环境
python -m venv .venv
source .venv/bin/activate  # macOS/Linux
# 或 .venv\Scripts\activate  # Windows

# 安装依赖
pip install -r requirements.txt
```

## 配置

在 `config` 目录下创建配置文件，设置 ComfyUI 服务器地址等参数。

## 启动

```bash
# HTTP 模式（默认）
python server.py --transport http --host 0.0.0.0 --port 18060

# 标准输入/输出模式
python server.py --transport stdio
```

### 启动参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--transport` | `http` | 传输模式：`stdio` 或 `http` |
| `--host` | `0.0.0.0` | 服务器监听地址 |
| `--port` | `18060` | 服务器端口 |
| `--path` | `/mcp` | HTTP 模式下的路径前缀 |
| `--show_banner` | `false` | 显示启动横幅 |

## Docker

```bash
docker-compose up -d
```

## 项目结构

```
comfyui-mcp-server/
├── server.py          # 主服务器入口
├── config/            # 配置文件目录
├── tools/             # MCP 工具实现
│   ├── generate_video.py
│   ├── generate_storyboard.py
│   ├── compose_video.py
│   ├── download_video.py
│   └── check_progress.py
├── utils/             # 工具类
│   ├── logger.py
│   └── comfy_client.py
└── workflows/         # ComfyUI 工作流配置
```

## 依赖

- Python 3.11+
- [FastMCP](https://github.com/jlowin/fastmcp)
- ComfyUI 服务器

## 许可证

MIT