# 04_making_real_projects

#### Create a web application project
##### Create package.json
```json
{
	"dependencies": {
		"express": "*"
	},
	"scripts": {
		"start": "node index.js"
	}
}
```

##### Create index.js
```javascript
const express = require("express")

const app = express();

app.get("/", (req, res) => {
	res.send("Hi there");
});

app.listen(8080, () => {
	console.log("Listening on port 8080")
});
```

##### Create Buildfile
```docker
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
```

#### Running our application in a container
##### Build our image
```console
docker build -t <DOCKERHUB_USERNAME>/<TAG> .
docker build -t yourusername/simpleweb .
```
Note that `<DOCKERHUB_USERNAME>/<TAG>` combination forms a `<DOCKER_IMAGE_TAG>` for our image.

##### Run docker with port forwarding
```console
docker run -p <PORT_NUMBER_ON_LOCALHOST>:<PORT_NUMBER_OF_THE_APP_IN_THE_CONTAINER> <DOCKER_IMAGE_TAG>
docker run -p 8080:8080 yourusername/simpleweb
```