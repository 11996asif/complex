# Stage 1: Build the application
FROM node:16-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json ./
COPY package-lock.json ./

# Install dependencies
RUN npm install

# Copy application files
COPY . .

# Build the application
RUN npm run build

# Stage 2: Serve the application
FROM nginx:latest

# Expose port
EXPOSE 3000

# Copy Nginx configuration file
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy built application files from builder stage
COPY --from=builder /app/build /usr/share/nginx/html
