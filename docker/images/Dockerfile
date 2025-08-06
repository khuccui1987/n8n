# === Stage 1: build các custom nodes trên Node 18 ===
FROM node:18-alpine AS builder

WORKDIR /custom
# Khởi tạo package.json tạm
RUN npm init -y

# Cài 2 package bạn cần vào node_modules
RUN npm install n8n-nodes-zalos-user n8n-nodes-debounce

# === Stage 2: build image n8n chính thức, chép custom nodes vào ===
FROM n8nio/n8n:latest

# cần root để copy file & chown
USER root

# Tạo thư mục chứa extensions
RUN mkdir -p /home/node/.n8n/custom

# Copy toàn bộ node_modules đã cài ở stage 1
COPY --from=builder /custom/node_modules /home/node/.n8n/custom/node_modules

# Set owner để n8n chạy không lỗi permission
RUN chown -R node:node /home/node/.n8n

# Quay về user node
USER node

WORKDIR /home/node

# Cho n8n biết có extension mới
ENV N8N_CUSTOM_EXTENSIONS=/home/node/.n8n/custom

# ENTRYPOINT/CMD mặc định image n8n đã sẵn sàng

EXPOSE 5678
