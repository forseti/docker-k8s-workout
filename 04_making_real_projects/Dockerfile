# Specify a base image
FROM node:alpine

# Specify a working directory
WORKDIR /opt/simpleweb

# Copy package.json into the container
COPY ./package.json ./

# Install some dependencies
RUN npm install

# Copy source files into the container
COPY ./ ./

# Default command
CMD ["npm", "start"]