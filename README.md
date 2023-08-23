# Continuous Integration

> Requires
> - Docker installed

## Args

| Arg             | Required | Default            | Description                                          |
|-----------------|----------|--------------------|------------------------------------------------------|
| --help          | false    |                    | Show available args.                                 |
| --authorization | false    | -                  | Storage api authorization token                      |
| --config        | false    | cd/deployment.yaml | Path to the deployment.yaml file.                    |
| --pushImage     | false    | true               | A flag to indicate whether to push the image or not. |

- Config build

```yaml
imageName: mya-pp
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

## Run

```shell
/deployment --authorization "your storage api authorization token"
```

