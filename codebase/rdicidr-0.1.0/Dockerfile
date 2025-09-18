# ---- Build stage ----
FROM node:15.14.0-buster AS build

WORKDIR /app

# Copy package files first
COPY package*.json ./

# Install dependencies without strict engine checks
RUN npm install --legacy-peer-deps --ignore-engines

# Copy source code
COPY . .

# Build React app
RUN npm run build


# ---- Run stage ----
FROM nginx:alpine

# Copy build output to Nginx HTML dir
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
