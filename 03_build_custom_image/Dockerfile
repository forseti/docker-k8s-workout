# Use an existing docker image as a base
FROM alpine

# Test the cache by swap position with redis
RUN apk add --update gcc

# Download and install a dependency
RUN apk add --update redis

# Tell the image what to do when it starts as a container
CMD ["redis-server"]