# Stage 1: Backend Builder
FROM node:21 AS backend-builder

# Set the working directory inside the container
WORKDIR /app

# Copy only package.json and package-lock.json to leverage Docker caching
COPY package.json package-lock.json ./

# Install production dependencies only
RUN NODE_ENV=development npm ci

# Copy the rest of the application files
COPY . .

# Stage 2: Slim Production Image
FROM node:21-slim

# Set the working directory
WORKDIR /app

# Copy built application and dependencies from the builder stage
COPY --from=backend-builder /app . 

# Expose the application port (5001)
EXPOSE 5001

# Start the server
CMD ["npm", "start"]

