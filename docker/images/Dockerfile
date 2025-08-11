# 1. Dùng official image
#-FROM n8nio/n8n:latest

# 2. Chuyển sang user root để cài node
#-USER root

# 3. Cài các node cần thiết
#RUN npm install n8n-nodes-zalos-user \
#    && npm install n8n-nodes-debounce
#RUN n8n install n8n-nodes-zalos-user n8n-nodes-debounce

# Cài node trực tiếp trong thư mục user mặc định của n8n
#RUN mkdir -p /home/node/.n8n && \
#    npm install --prefix /home/node/.n8n \
#      n8n-nodes-zalos-user \
#      n8n-nodes-debounce

#RUN mkdir -p /home/node/.n8n/custom && \
#    npm install \
#      n8n-nodes-zalos-user \
#      n8n-nodes-debounce \
#      --prefix /home/node/.n8n/custom

#RUN npm install n8n-nodes-debounce n8n-nodes-zalos-user

# 4. Trả lại quyền chạy cho user node
#-USER node

# 5. Expose port
#-EXPOSE 5678


FROM n8nio/n8n:1.105.4

USER root
RUN apk add --no-cache bash \
    && npm prune --production \
    && rm -rf /root/.npm /tmp/*

ENV PATH=/usr/local/bin:$PATH

USER node
WORKDIR /data

ENV NODE_ENV=production \
    N8N_DIAGNOSTICS_ENABLED=false \
    N8N_TELEMETRY_DISABLED=true \
    N8N_LOG_LEVEL=warn \
    EXECUTIONS_PROCESS=main \
    N8N_CONCURRENCY=2 \
    NODE_OPTIONS="--max-old-space-size=512 --expose-gc"

EXPOSE 5678
CMD ["node", "--max-old-space-size=512", "node_modules/n8n/bin/n8n"]
