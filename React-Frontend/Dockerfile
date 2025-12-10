# ----- Stage 1: Build -----
FROM node:18 AS builder

# Set working directory inside container
WORKDIR /app

# Copy dependency files and install
COPY package*.json ./
RUN npm install

# Copy the full source code
COPY . .

# Build the Vite application
RUN npm run build

# ----- Stage 2: Runtime -----
FROM nginx:alpine AS runtime

# Remove default Nginx config that conflicts with custom config
# RUN rm /etc/nginx/conf.d/default.conf

# Copy dist folder from the builder stage
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy provided nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf

# Run Nginx
CMD ["nginx", "-g", "daemon off;"]