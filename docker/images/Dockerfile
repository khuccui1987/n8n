# 1. Dùng official image
FROM n8nio/n8n:latest

# 2. Chuyển sang user root để cài node
USER root

# 3. Cài các node cần thiết
#RUN npm install n8n-nodes-zalos-user \
#    && npm install n8n-nodes-debounce
#RUN n8n install n8n-nodes-zalos-user n8n-nodes-debounce

# Cài node trực tiếp trong thư mục user mặc định của n8n
#RUN mkdir -p /home/node/.n8n && \
#    npm install --prefix /home/node/.n8n \
#      n8n-nodes-zalos-user \
#      n8n-nodes-debounce

RUN mkdir -p /home/node/.n8n/custom && \
    npm install \
      n8n-nodes-zalos-user \
      n8n-nodes-debounce \
      --prefix /home/node/.n8n/custom

# 4. Trả lại quyền chạy cho user node
#USER node

# 5. Expose port
EXPOSE 5678
