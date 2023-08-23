# Continuous Integration

> Requires
> - Docker installed

## Args

| Arg             | Required | Default            | Description                                                                                                                     |
|-----------------|----------|--------------------|---------------------------------------------------------------------------------------------------------------------------------|
| --help          | false    |                    | Show available args.                                                                                                            |
| --config        | false    | cd/deployment.yaml | Path to the deployment.yaml file.                                                                                               |
| --pushImage     | false    | true               | A flag to indicate whether to push the image or not. If true the generate docker image and docker-compose.yaml, will be pushed. |
| --imageTag      | false    |                    | The imageTag parameter is used during the Docker image build process to tag the image that is being built.                      |
| --authorization | false    | -                  | Storage api authorization token                                                                                                 |

- Config build

```yaml
imageName: mya-pp

# By running /deployment specifying --imageTag, the imageTag on configuration file will be ignored 
imageTag: v1
template: "ci/deployment.mustache"

# Expecting endpoint that accept post file with body like to 
# push the new docker-compose.yaml file
# curl --location 'https://storage-api.com/v1/file/upload' \
#--header 'Authorization: oauthToken' \
#  --form 'file=@"my-file-path"' \
#  --form 'fileName="my-file-name"' \
#  --form 'dirName="directory-destiny"'
uploadUrl: https://storage-api.com/v1/file/upload
# If you want to push the image to a custom docker registry
pushImageHost: docker-registry.com
# If you want to pull the image from a custom docker registry
pullImageHost: 127.0.0.1:5000
dockerfile: .
bind:
  ports:
    - "127.0.0.1:8080:80"
    - "172.17.0.1:8080:80"
  volumes:
    - ~/.storage/:/root/.storage/
limit:
  memory: 2G
  cpu: 0.5
volumes:
  - "example_logs:"
```

## Get authorization token

- By request authorization from script `authorization`, the api must return a response like json bellow, by a `POST`
  method declared in `{{apitHost}}`

```json
{
  "code": 200,
  "success": true,
  "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
  "message": "Authorization successful.",
  "timestamp": 1692678504740
}
```

```shell
export AUTHORISATION=$(./ci/authorization -api_host {{apitHost}} -password {{password}} -username {{username}})
```

## Run

```shell
/deployment --authorization $AUTHORIZATION
```

