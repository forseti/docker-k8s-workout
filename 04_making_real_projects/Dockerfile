# Specify a base image
FROM node:alpine

# Specify a working directory
WORKDIR /opt/simpleweb

# Copy source files into the container
COPY ./ ./

# Install some dependencies
RUN npm install

# Default command
CMD ["npm", "start"]