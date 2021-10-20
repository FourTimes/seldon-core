seldon trial installtion steps

sudo apt install apache2-utils
mkdir -p ${HOME}/.config/seldon/seldon-deploy/
vim ${HOME}/.config/seldon/seldon-deploy/sdconfig.txt

```txt

GIT_USER="xxxxxx"
GIT_TOKEN="xxxxxx"
GIT_EMAIL="jjino@xxxx.com"
ENABLE_GIT_SSH_CREDS=false
SD_USER_EMAIL="admin@seldon-ey.io"
SD_PASSWORD="ChangeMe@123"
XTERNAL_HOST=                             # This can be blank
EXTERNAL_PROTOCOL=http                    # "https" or "http"
KFSERVING_PROTOCOL=$EXTERNAL_PROTOCOL
MULTITENANT=false                         # Restricts permissions to namespace-level. Ask seldon before using.
ENABLE_APP_AUTH=true                      # 'true' or 'false'
VIRTUALSERVICE_CREATE=true
ENABLE_METADATA_POSTGRES=true             # If false will skip installing PostgreSQL in the trial cluster and metadata API will be unavailable.
ENABLE_OPA=false                          # If true will fetch OPA policies from a `seldon-deploy-policies` config map from the namespace Deploy is running in.
ENABLE_PROJECT_BASED_AUTH=false           # If true will authorize requests to resources based on what access does the user have to all models in that resource.
ENABLE_AUDIT=true                         # If true will setup a fluentd instance to forward Deploy's audit logs to a minio bucket.

```
 Use the following script to check or create an initial file to fill in.

```bash

cd seldon-deploy-install
./check-config


# Default Trial Installation¶

TAG=1.4.0 && \
    docker create --name=tmp-sd-container seldonio/seldon-deploy-server:$TAG && \
    docker cp tmp-sd-container:/seldon-deploy-dist/seldon-deploy-install.tar.gz . && \
    docker rm -v tmp-sd-container

tar -xzf seldon-deploy-install.tar.gz


cd seldon-deploy-install
./prerequisites-setup/default-setup.sh
./sd-setup/sd-install-default






```

