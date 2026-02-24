# Backend Dockerfile - Node.js + Express API
# Simple single-stage: no compilation needed for plain JavaScript

FROM node:18-alpine

WORKDIR /app

# Copy package files first (layer cache optimization)
COPY package*.json ./

# Install production dependencies only (smaller image, faster)
RUN npm install --production

# Copy all backend source files
COPY . .

# Port our Express server listens on (matches server.js)
EXPOSE 8080

# Start the Express server
CMD ["node", "server.js"]