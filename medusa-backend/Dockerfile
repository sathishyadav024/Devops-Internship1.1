# Dockerfile
FROM node:18

# Set working directory
WORKDIR /app

# Install Medusa CLI globally
RUN npm install -g @medusajs/medusa-cli

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the application port
EXPOSE 9000

# Start the Medusa server
CMD ["medusa", "develop"]

