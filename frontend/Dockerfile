# =========================
# 1) Build stage
# =========================
FROM node:18-alpine AS build
WORKDIR /app

# Reduce npm noise
ENV NPM_CONFIG_AUDIT=false \
    NPM_CONFIG_FUND=false \
    NPM_CONFIG_UPDATE_NOTIFIER=false \
    NPM_CONFIG_LOGLEVEL=error\
    NODE_OPTIONS="--max_old_space_size=1536"

# Install dependencies (better caching)
COPY package*.json ./
RUN npm ci --no-audit --no-fund

# Copy source and build
COPY . .
RUN npm run build

# =========================
# 2) Runtime stage (nginx)
# =========================
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Clean default nginx content
RUN rm -rf ./*

# ✅ IMPORTANT: Copy the correct dist folder
# Your dist folder is: dist/angular-ecommerce
COPY --from=build /app/dist/angular-ecommerce/ ./

# SPA routing fix (so refresh works)
RUN printf '%s\n' \
'server {' \
'  listen 80;' \
'  server_name _;' \
'  root /usr/share/nginx/html;' \
'  index index.html;' \
'  location / {' \
'    try_files $uri $uri/ /index.html;' \
'  }' \
'}' > /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
