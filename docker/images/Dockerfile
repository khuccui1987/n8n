# 1. Base image chính thức của n8n (mới nhất)
FROM n8nio/n8n:latest

# 2. Chuyển sang root để cài package
USER root

# 3. Cài pnpm và dùng pnpm để cài 2 custom nodes
RUN npm install -g pnpm@latest \
    && pnpm add -g n8n-nodes-zalos-user n8n-nodes-debounce \
    \
    # 4. Dọn cache npm & pnpm để giảm dung lượng image
    && npm cache clean --force \
    && pnpm store prune \
    \
    # 5. Chuyển ownership các thư mục để user `node` có thể đọc/write
    && chown -R node:node /home/node/.npm /home/node/.pnpm-store /usr/local/lib/node_modules /usr/local/bin

# 6. Quay về user node an toàn hơn
USER node

# 7. (Tùy chọn) Đặt WORKDIR về thư mục mặc định
WORKDIR /home/node

# CMD/ENTRYPOINT mặc định của n8n sẽ tự chạy, không cần khai báo lại


EXPOSE 5678
