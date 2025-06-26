# 1. Dùng official image
FROM n8nio/n8n:latest

# 2. Chuyển sang user root để cài node
USER root

# 3. Cài các node cần thiết
RUN npm install n8n-nodes-zalos-user \
    && npm install n8n-nodes-debounce

# 4. Trả lại quyền chạy cho user node
USER node

# 5. Expose port
EXPOSE 5678
