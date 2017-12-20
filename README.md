# GitLab CI runner that rsyncs to remote server

This GitLab CI runner image allows to sync a GitLab project to a remote location (running ssh server) via rsync (useful for Doxygen, etc.)

## How to use

Create `.gitlab-ci.yml`:

```yaml
image: alpine

before_script:
- apk update
- apk add doxygen
- apk add ttf-freefont graphviz
- apk add 
- apk add openssh-client

stages:
  - deploy

deploy to production:
  stage: deploy
  environment: production
  only:
    - master
  script: rsync-script.sh dokku@dokku.me:myapp my_local/path
```

Go to GitLab > Project > Settings > CI/CD Pipelines > Secret Variables, and add a variable `SSH_PRIVATE_KEY`:

```
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```


