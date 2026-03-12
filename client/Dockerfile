# Multi-stage build for React (Vite) client

# Stage 1: build the app
FROM node:18-alpine AS builder
WORKDIR /app

# copy package files and install dependencies
COPY package.json package-lock.json* ./
RUN npm install

# copy source and build
COPY . .
RUN npm run build

# Stage 2: serve with nginx
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html

# expose http port
EXPOSE 80

# run nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
