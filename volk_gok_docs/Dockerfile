# Dockerfile for docs service
# Simple Node.js HTTP server serving documentation

FROM node:18-alpine

# Install dumb-init for proper signal handling
RUN apk add --no-cache dumb-init

# Set working directory
WORKDIR /app

# Copy application files
COPY server.js ./
COPY *.html ./
COPY data.json ./
COPY screenshots/ ./screenshots/

# Create screenshots directory if it doesn't exist
RUN mkdir -p screenshots

# Expose port 3000
EXPOSE 3000

# Use dumb-init to handle signals properly
ENTRYPOINT ["dumb-init", "--"]

# Start the server
CMD ["node", "server.js"]