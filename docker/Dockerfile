# 使用国内镜像源 (DaoCloud)
FROM m.daocloud.io/docker.io/library/python:3.12-slim

# 设置工作目录
WORKDIR /app

# 配置国内 pip 镜像源
RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 拷贝 requirements.txt 先安装依赖
COPY requirements.txt .

# 安装依赖
RUN pip install --no-cache-dir -r requirements.txt

# 安装 ffmpeg (使用阿里云源)
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list.d/debian.sources && \
    sed -i 's|security.debian.org|mirrors.aliyun.com|g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update && apt-get install -y ffmpeg && rm -rf /var/lib/apt/lists/*

# 拷贝项目文件
COPY . .

# 暴露端口
EXPOSE 18060

# 启动 MCP Server
CMD ["python", "server.py"]