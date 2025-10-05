ARG NODE_VERSION=21.7.2

FROM node:${NODE_VERSION}-alpine AS builder

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm ci

COPY . .

# Build the Vite app (output goes to /usr/src/app/dist)
RUN npm run build

# ======================
# Stage 2: Runtime
# ======================

FROM nginx:alpine 

# Copy built files from builder
COPY --from=builder /usr/src/app/dist /usr/share/nginx/html

# Expose the port that the application listens on.
EXPOSE 80

# Nginx serves index.html by default
CMD ["nginx", "-g", "daemon off;"]
