# ---- Build Stage ----
FROM node:20 AS builder  
WORKDIR /app

# Install deps
COPY package*.json ./
RUN npm install

# Copy all project files
COPY . .

# Build Vite → generates /dist
RUN npm run build

# ---- Production Stage ----
FROM nginx:stable-alpine

# Copy the built dist folder from previous step
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose web port
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
