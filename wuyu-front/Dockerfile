# 构建阶段
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# 运行阶段（使用 Node.js 内置 http-server 或 serve）
FROM node:18-alpine
RUN npm install -g serve  # 安装静态文件服务器
COPY --from=build /app/dist /app/dist
EXPOSE 8080
CMD ["serve", "-s", "dist", "-l", "9180"]
