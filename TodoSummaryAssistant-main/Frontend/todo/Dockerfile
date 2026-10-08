# Stage 1: Build React app
FROM node:18-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
USER appuser
CMD ["nginx", "-g", "daemon off;"]
