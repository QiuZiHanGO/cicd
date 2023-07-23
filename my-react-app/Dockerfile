# Stage 1: 构建阶段
# 使用Node镜像作为构建阶段基础镜像
FROM node:latest

# 设置工作目录
WORKDIR /app

# 将package.json和package-lock.json复制到容器中，并安装依赖
COPY package*.json ./
RUN npm install

# 复制项目文件到容器中
COPY . .

# 构建React项目
RUN npm run build

# Stage 2: 生产阶段
# 使用Nginx镜像作为生产阶段基础镜像
FROM nginx:latest

# 将构建阶段中生成的静态文件复制到Nginx的默认静态文件目录
COPY --from=builder /app/build /usr/share/nginx/html

# Nginx默认监听的端口为80，因此不需要额外暴露端口

# 容器启动时执行的命令
CMD ["nginx", "-g", "daemon off;"]
