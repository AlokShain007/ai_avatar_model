# Use Node.js base image for building the frontend
FROM node:18 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and yarn.lock files
COPY package.json yarn.lock ./

# Install dependencies
RUN yarn install

# Copy the rest of the project files
COPY . .

# Build the frontend for production
RUN yarn build

# Use Nginx to serve the built files
FROM nginx:alpine

# Copy the build output from the build container to Nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80 to the outside world
EXPOSE 80

# Start Nginx in the foreground (default entrypoint of the Nginx container)
CMD ["nginx", "-g", "daemon off;"]
