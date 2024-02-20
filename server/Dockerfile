# Node base image
FROM node:current-alpine3.18

# Set the working directory
WORKDIR /app

# Install dependencies
# Make sure package.json and yarn.lock (if present) are in the same directory as the Dockerfile
COPY package.json yarn.lock* ./
RUN yarn install --frozen-lockfile

# Copy the rest of the backend code
COPY . .

# Your backend now listens on port 5000
EXPOSE 5000

# Start the backend server
CMD ["yarn", "start"]
