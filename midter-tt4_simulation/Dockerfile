# Layer 1: Builder
FROM node:latest AS builder
WORKDIR /app
COPY ./app/package*.json ./
RUN npm install
COPY ./app/ ./
RUN npm run build  # This will create the /dist directory

# Layer 2: Nginx server
FROM nginx

# Copy the build output to Nginx's public directory
COPY --from=builder ./app/dist /usr/share/nginx/html

# Copy custom Nginx configuration to use the correct port
COPY default.conf /etc/nginx/conf.d/

# Expose the custom port
EXPOSE 8080

# Start Nginx (default command)
CMD ["nginx", "-g", "daemon off;"]
