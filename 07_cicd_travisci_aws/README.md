# 07_cicd_travisci_aws
#### Branch location
Due to limitation in Travis CI, this project is hosted independently at https://github.com/forseti/dkw_07_docker_travisci_aws

#### Some Tips
##### Running test on CI Server
Set environment variable CI=true for Jest
```console
docker run -e CI=true yourusername/frontend npm run test -- --coverage
```