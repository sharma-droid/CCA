# ------------------- Stage 1: Build Stage ------------------------------
FROM node:20 AS frontend-builder

# Set the working directory to /app
WORKDIR /app

# Copy the package.json and package-lock.json for dependency installation
COPY package.json ./

# Install dependencies
RUN npm install

RUN npm run build

# Copy the rest of the application code
COPY frontend/build/ .

# ------------------- Stage 2: Final Stage ------------------------------
FROM node:20-slim

# Set the working directory to /app
WORKDIR /app

# Copy built assets and dependencies from frontend-builder stage
COPY --from=frontend-builder /app .

# Copy the .env.sample file to .env.local
# COPY .env .env

# Expose port 3000 for the Node.js application
EXPOSE 3000

# Define the default command to run the application in development mode
CMD ["npm", "run", "dev"]