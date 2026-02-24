# frontend/Dockerfile
# =============================================
# STAGE 1: BUILD
# Node.js image to compile Angular TypeScript
# into plain HTML/CSS/JS files
# =============================================
FROM node:18-alpine AS build

WORKDIR /app

# Copy package files first (Docker cache optimization)
# If these don't change, npm install won't re-run = faster builds
COPY package*.json ./

RUN npm install

# Copy all source code
COPY . .

# Build Angular app for production
# Output goes to: /app/dist/angular-15-crud/
RUN npm run build

# =============================================
# STAGE 2: SERVE
# Tiny nginx image to serve the built files
# Node.js is NOT needed to serve static files
# nginx is much smaller and faster for this
# =============================================
FROM nginx:alpine

# Remove default nginx welcome page config
RUN rm /etc/nginx/conf.d/default.conf

# Copy our custom nginx config
COPY nginx.conf /etc/nginx/conf.d/

# ⚠️  KEY FIX: Copy the correct build output folder
# Angular project name is "angular-15-crud" so output is dist/angular-15-crud
# NOT dist/frontend — that was the error!
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]