# Build stage for the React application
FROM node:current-alpine3.18 AS build-stage

# Set the working directory
WORKDIR /app

# Install build dependencies for native modules
RUN apk add --no-cache python3 make g++ && \
    # Clean up unnecessary cache files
    rm -rf /var/cache/apk/*

# Copy package.json and package-lock.json (or yarn.lock)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of your application's code
COPY . .

# Build the application
RUN npm run build

# Stage 2: Serve the app with Nginx
FROM nginx:stable-alpine AS production-stage

# Copy the built app to Nginx's serve directory
COPY --from=build-stage /app/build /usr/share/nginx/html

# Expose port 80 to the outside once the container has launched
EXPOSE 80

# The command to run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
