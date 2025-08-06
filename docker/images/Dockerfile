# 1) Dùng image n8n base (nếu muốn node 18 cho an toàn, có thể đổi thành n8nio/n8n:1.50.2-node18)
FROM n8nio/n8n:latest

# 2) Chạy dưới root để cài tool
USER root

# 3) Tắt strict engine, cài pnpm và only-allow
ENV NPM_CONFIG_ENGINE_STRICT=false
RUN npm install -g pnpm@latest only-allow@latest

# 4) Dùng pnpm để install global các custom nodes
RUN pnpm add -g n8n-nodes-zalos-user n8n-nodes-debounce

# 5) Dọn cache để giảm kích thước image
RUN pnpm store prune && npm cache clean --force

# 6) Chuyển ownership về node user
RUN chown -R node:node \
      /home/node/.npm \
      /home/node/.pnpm-store \
      /usr/local/lib/node_modules \
      /usr/local/bin

# 7) Quay về user node
USER node

# 8) (Tùy chọn) WORKDIR
WORKDIR /home/node

# 9) Kích hoạt custom extensions nếu chưa set
ENV N8N_CUSTOM_EXTENSIONS=/home/node/.n8n/custom

# CMD/ENTRYPOINT gốc của n8n vẫn được giữ, không cần khai báo lại


EXPOSE 5678
