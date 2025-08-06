### Dockerfile for n8n with custom nodes on Node 18

# 1) Use a Node 18-compatible base image of n8n
FROM n8nio/n8n:1.50.2-node18

# 2) Switch to root for installations
USER root

# 3) Disable strict engine checks, install pnpm and only-allow globally
ENV NPM_CONFIG_ENGINE_STRICT=false
RUN npm install -g pnpm@latest only-allow@latest

# 4) Use pnpm to install custom nodes globally
RUN pnpm add -g n8n-nodes-zalos-user n8n-nodes-debounce

# 5) Clean up caches to reduce image size
RUN pnpm store prune && npm cache clean --force

# 6) Fix permissions so `node` user can access installed modules
RUN chown -R node:node \
      /home/node/.npm \
      /home/node/.pnpm-store \
      /usr/local/lib/node_modules \
      /usr/local/bin

# 7) Drop back to non-root `node` user for security
USER node

# 8) Ensure working directory is set
WORKDIR /home/node

# 9) Enable custom extensions directory if used
ENV N8N_CUSTOM_EXTENSIONS=/home/node/.n8n/custom

# 10) The default ENTRYPOINT/CMD from the base image will run n8n

EXPOSE 5678
