# GITLAB REGISTRY CLEANER
### Decription
Have a couple Kubernetes clusters and GitLab registry full of unused images. Case is delete unused images from GitLab and keep images used by apps in Kubernetes.

### Resources
 * `CPU_REQUEST = 0.05`
 * `RAM_REQUEST = 64` Mb
 * `CPU_LIMIT = 0.5`
 * `RAM_LIMIT = 128` Mb

### Local Run
 * `python3.9 start.py`
 
### Build
  * ```
    docker build -t gitlab-regcleaner .
    ```
    or
  * ```
    docker-compose up --build
    ```
 
### Environment variables
 * `GIT_TOKEN=asdasdasd` - GitLab token (api,read_repository, read_registry)
 * `KubeStageConfigPath=/app/stage.conf` - kubernetes config path (recomended permissions -  get, list, watch)
 * `KubeProdConfigPath=/app/prod.conf` - kubernetes config path. If you have more then 2 clusters or just 1 please edit string 85 start.py. If you only have one cluster, set `KubeStageConfigPath` and `KubeProdConfigPath` to empty (or not declare)
 * `KubeConfigPath=/app/kube-config.conf` - kubernetes config path. Must be declared for empty variables `KubeStageConfigPath` and `KubeProdConfigPath`
 * `MAX_CONNECTIONS=50` - parametr limits max simultaneous sessions for async framework.
 * `GITLAB_PROTO=https` - protocol for connecting to the self-hosted gitlab host (`http` or `https`)
 * `GITLAB_HOSTNAME=gitlab.my.ru` - hostname of your GitLab.
 * `EXCLUDE_PROJECTS=project1,project2` - add projects that must be excluded (projects with Job, CronJob or just store of valuable unused images) from search or leave it blank.
 * `ONLY_THIS_GROUP=https://gitlab.my.ru/dev` - if you need to clean only one group or leave it blank.
 * `KUBE_HISTORY=5` - how much images from rollout history you want to keep.
 * `REMOVE_UNUSED_TAGS=false` - false - inspect,  true - remove unused images.
