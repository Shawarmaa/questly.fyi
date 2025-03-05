# Use an official Node.js runtime as a parent image
FROM node:18-alpine AS builder

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install app dependencies
RUN npm install --legacy-peer-deps

# Copy all source code
COPY . .

# Build the Next.js app for production
RUN npm run build

# Serve the app using a lightweight web server (e.g., Nginx or node server)
FROM node:18-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the build output from the builder stage
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./package.json

# Install production dependencies
RUN npm install --production --legacy-peer-deps

# Expose port 3000 (or the port your Next.js app uses)
EXPOSE 3000

# Set the command to start the Next.js app
CMD ["npm", "start"]