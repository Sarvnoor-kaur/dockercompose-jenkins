# Use slim base image
FROM node:18-alpine

WORKDIR /app

# Copy dependency files first (for caching)
COPY package*.json ./

# Install production dependencies only
RUN npm ci --only=production

# Copy application code
COPY . .

EXPOSE 5000

CMD ["node", "server.js"]