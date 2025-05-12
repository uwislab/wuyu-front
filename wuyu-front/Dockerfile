# 使用 Node.js 作为构建环境
FROM node:18-alpine AS builder

# 设置工作目录
WORKDIR /app

# 复制项目文件到容器
COPY package*.json ./
COPY . .

# 安装依赖并构建
RUN npm ci && npm run build

# 使用 Nginx 作为生产环境
FROM nginx:alpine

# 从构建阶段复制构建产物
COPY --from=builder /app/dist /usr/share/nginx/html

# 复制自定义 Nginx 配置（如果需要处理路由）
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 暴露端口
EXPOSE 80

# 启动 Nginx
CMD ["nginx", "-g", "daemon off;"]
