
# 1. Lấy base image chính thức của n8n
FROM n8nio/n8n:latest

# 2. Chuyển sang root để có quyền cài đặt
USER root

# 3. Cài thêm 2 node package toàn cục
RUN npm install --location=global \
      n8n-nodes-zalos-user \
      n8n-nodes-debounce \
    && npm cache clean --force \
    # đảm bảo quyền sở hữu về node user để n8n có thể truy cập
    && chown -R node:node /home/node/.npm

# 4. Trả lại quyền cho node user (mặc định bên trong image n8n)
USER node

# 5. (Tùy chọn) Đặt WORKDIR về thư mục của n8n
WORKDIR /home/node

# 6. ENTRYPOINT và CMD mặc định sẽ tự chạy n8n, không cần khai báo lại

EXPOSE 5678
