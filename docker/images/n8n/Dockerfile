FROM node:18-alpine

RUN apk add --no-cache bash python3 make g++ \
    && npm install -g yarn

RUN yarn add n8n@1.105.4 --production

RUN addgroup -S n8n && adduser -S n8n -G n8n
USER n8n
WORKDIR /data

ENV NODE_ENV=production \
    N8N_DIAGNOSTICS_ENABLED=false \
    N8N_TELEMETRY_DISABLED=true \
    N8N_LOG_LEVEL=warn \
    NODE_OPTIONS="--max-old-space-size=512 --expose-gc"

EXPOSE 5678
CMD ["node", "--max-old-space-size=512", "node_modules/n8n/bin/n8n"]
