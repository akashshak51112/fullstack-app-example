FROM node:20-alpine AS build

# Set working directory
WORKDIR /app


COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application source code
COPY . .

# Build the frontend (assumes a React/Vite/Next.js app with 'build' script)
RUN npm run build

# Use an official Nginx image to serve the built app
FROM nginx:alpine

# Copy built assets from the build stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]