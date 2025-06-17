FROM alpine:3.19 AS builder

# 下载架构特定的二进制文件
RUN apk --no-cache add curl && \
    mkdir -p /app && \
    if [ "$(uname -m)" = "x86_64" ]; then \
        curl -s -L -k --connect-timeout 30 --retry 3 -o /app/nx-app https://github.com/dsadsadsss/plutonodes/releases/download/xr/linux-amd64-nx-app.bin; \
    elif [ "$(uname -m)" = "aarch64" ]; then \
        curl -s -L -k --connect-timeout 30 --retry 3 -o /app/nx-app https://github.com/dsadsadsss/plutonodes/releases/download/xr/linux-arm64-nx-app.bin; \
    else \
        echo "Unsupported architecture"; \
        exit 1; \
    fi && \
    chmod +x /app/nx-app

FROM alpine:3.19

# 设置环境变量
ENV PORT="8080" NX_PORT="3555" VM_PORT="8001" VL_PORT="8002" \
    MPATH="vms" VPATH="vls" NEZ_KEY="zmmznnzzm" URL="mirror.umd.edu"

# 工作目录
WORKDIR /app

# 安装必要的依赖
RUN apk --no-cache add supervisor bash nginx && \
    mkdir -p /var/log/supervisor /etc/supervisor.d && \
    # 创建启动脚本
    echo '#!/bin/bash' > /app/start.sh && \
    echo 'sed -i \' >> /app/start.sh && \
    echo '  -e "s/8080/${PORT}/g" \' >> /app/start.sh && \
    echo '  -e "s/8001/${VM_PORT}/g" \' >> /app/start.sh && \
    echo '  -e "s/8002/${VL_PORT}/g" \' >> /app/start.sh && \
    echo '  -e "s/3555/${NX_PORT}/g" \' >> /app/start.sh && \
    echo '  -e "s/vms/${MPATH}/g" \' >> /app/start.sh && \
    echo '  -e "s/vls/${VPATH}/g" \' >> /app/start.sh && \
    echo '  -e "s/zmmznnzzm/${NEZ_KEY}/g" \' >> /app/start.sh && \
    echo '  -e "s#\${URL}#${URL}#g" \' >> /app/start.sh && \
    echo '  /app/nginx.conf' >> /app/start.sh && \
    echo 'mv -f /app/nginx.conf /etc/nginx/nginx.conf' >> /app/start.sh && \
    echo 'exec /usr/bin/supervisord -c /etc/supervisord.conf' >> /app/start.sh && \
    chmod +x /app/start.sh && \
    rm -rf /var/cache/apk/* /tmp/*

# 从builder阶段复制应用程序
COPY --from=builder /app/nx-app /app/nx-app

# 复制配置文件
COPY supervisord.conf /etc/supervisord.conf
COPY damon.ini /etc/supervisor.d/damon.ini
COPY nginx.conf /app/nginx.conf

EXPOSE ${PORT}

# 启动supervisord
CMD ["/app/start.sh"]
