# 构建阶段
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# 运行阶段（使用 Node.js 内置 http-server 或 serve）
FROM node:18-alpine
RUN npm install -g serve  # 安装轻量级静态服务器
COPY --from=build /app/dist /app/dist
EXPOSE 8080  # 指定容器监听端口为 8080
CMD ["serve", "-s", "dist", "-l", "8080"]  # 启动服务并监听 8080
