# Continuous Integration

> Requires
> - Docker installed

## Args

| Arg               | Required | Default            | Description                                                                                                                     |
|-------------------|----------|--------------------|---------------------------------------------------------------------------------------------------------------------------------|
| -loginUsername    | false    |                    | Docker login username, if provided username and password, will try to login on Docker.                                          |
| -loginPassword    | false    |                    | Docker login password, if provided username and password, will try to login on Docker.                                          |
| -help             | false    |                    | Show available args.                                                                                                            |
| -config           | false    | cd/deployment.yaml | Path to the deployment.yaml file.                                                                                               |
| -pushImage        | false    | true               | A flag to indicate whether to push the image or not. If true the generate docker image and docker-compose.yaml, will be pushed. |
| -imageTag         | false    |                    | The imageTag parameter is used during the Docker image build process to tag the image that is being built.                      |
| -storeImageAsFile | false    | false              | If true, the image will be stored as a file.                                                                                    |
| -fileName         | false    | docker-image.tar   | If storeImageAsFile is true, the image will be stored as a file with the name provided in fileName.                             |

- [Deployment configuration example](https://github.com/softwareplace/docker-deployment/blob/main/deployment.yaml)
