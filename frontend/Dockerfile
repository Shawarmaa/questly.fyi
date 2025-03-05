# Stage 1: Build the Next.js app
FROM node:18-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package.json and lock file
COPY package*.json ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Copy application files
COPY . .

# Build Next.js app
RUN npm run build

# Stage 2: Run the app
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy built files from the builder stage
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./package.json

# Install all dependencies (not just production)
RUN npm install --legacy-peer-deps

# Expose port
EXPOSE 3000

# Start the Next.js production server
CMD ["npm", "run", "start"]