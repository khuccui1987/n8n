# ===== Stage 1: Build =====
FROM node:18-alpine AS builder

# Cài đặt các tool cần thiết để build
RUN apk add --no-cache python3 make g++

# Tạo thư mục làm việc
WORKDIR /data

# Copy package.json và package-lock.json trước
COPY package*.json ./

# Cài dependencies (không cài devDependencies để tiết kiệm RAM/dung lượng)
RUN npm ci --only=production

# Copy toàn bộ source
COPY . .

# ===== Stage 2: Runtime =====
FROM node:18-alpine

# Thêm bash nếu cần debug
RUN apk add --no-cache bash

# Thiết lập môi trường n8n
ENV NODE_ENV=production \
    N8N_DIAGNOSTICS_ENABLED=false \
    N8N_TELEMETRY_DISABLED=true \
    N8N_LOG_LEVEL=warn \
    N8N_DEFAULT_LOCALE=en \
    NODE_OPTIONS="--max-old-space-size=512 --expose-gc"

# Tạo user không chạy dưới root
RUN addgroup -S n8n && adduser -S n8n -G n8n
USER n8n

WORKDIR /data

# Copy từ stage build
COPY --from=builder /data /data

# Expose port
EXPOSE 5678

# Lệnh khởi chạy
CMD ["node", "--max-old-space-size=512", "node_modules/n8n/bin/n8n"]
