FROM node:18-alpine

RUN apk add --no-cache bash

ENV NODE_ENV=production \
    N8N_DIAGNOSTICS_ENABLED=false \
    N8N_TELEMETRY_DISABLED=true \
    N8N_LOG_LEVEL=warn \
    N8N_DEFAULT_LOCALE=en \
    NODE_OPTIONS="--max-old-space-size=512 --expose-gc"

RUN addgroup -S n8n && adduser -S n8n -G n8n
USER n8n

WORKDIR /data

# Cài n8n trực tiếp từ npm (chỉ bản production)
RUN npm install n8n@1.105.4 --omit=dev

EXPOSE 5678

CMD ["node", "--max-old-space-size=512", "node_modules/n8n/bin/n8n"]
