FROM node:16-alpine AS build

WORKDIR /app

# Copy package files first for better caching
COPY package*.json ./
RUN npm install

# Copy the rest of the source code
COPY . .

# Build optimized React production bundle
RUN npm run build

# ---- Run stage ----
FROM nginx:alpine

# Copy build artifacts from previous stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 8080 (challenge requirement)
EXPOSE 8080

# Replace default nginx config to listen on 8080
RUN sed -i 's/listen       80;/listen       8080;/g' /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off;"]
