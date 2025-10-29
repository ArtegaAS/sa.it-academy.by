# 08. Docker. Docker compose
## Homework Assignment 1: Docker Compose for Application Stacks

### 6. Document the Docker Compose file structure and the steps to deploy the application stack.

```
08.Docker.Docker-compose
 └──HA1/
     ├──app/
     │   ├── Dockerfile
     │   └── app.py
     └── docker-compose.yml
```
__Input__
```
sudo docker compose up -d --build
curl http://localhost:5000
```

__Output__
```
WARN[0000] /home/student/08.DockerСompose/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Building 1.2s (12/12) FINISHED
 => [internal] load local bake definitions                                                                                                                                                                            0.0s
 => => reading from stdin 525B                                                                                                                                                                                        0.0s
 => [internal] load build definition from Dockerfile                                                                                                                                                                  0.0s
 => => transferring dockerfile: 170B                                                                                                                                                                                  0.0s
 => [internal] load metadata for docker.io/library/python:3.11-slim                                                                                                                                                   1.0s
 => [internal] load .dockerignore                                                                                                                                                                                     0.0s
 => => transferring context: 2B                                                                                                                                                                                       0.0s
 => [1/5] FROM docker.io/library/python:3.11-slim@sha256:8eb5fc663972b871c528fef04be4eaa9ab8ab4539a5316c4b8c133771214a617                                                                                             0.0s
 => [internal] load build context                                                                                                                                                                                     0.0s
 => => transferring context: 93B                                                                                                                                                                                      0.0s
 => CACHED [2/5] WORKDIR /app                                                                                                                                                                                         0.0s
 => CACHED [3/5] COPY requirements.txt .                                                                                                                                                                              0.0s
 => CACHED [4/5] RUN pip install -r requirements.txt                                                                                                                                                                  0.0s
 => CACHED [5/5] COPY . .                                                                                                                                                                                             0.0s
 => exporting to image                                                                                                                                                                                                                      0.0s
 => => exporting layers                                                                                                                                                                                                                       0.0s
 => => writing image sha256:4b28f303f8e473d1fac31f6ba6aceca85cd7a0e40b00bbf6396854c09d1c6815                                                                                                                          0.0s
 => => naming to docker.io/library/08dockerompose-web                                                                                                                                                                 0.0s
 => resolving provenance for metadata file                                                                                                                                                                            0.0s
[+] Running 3/3
 ✔ 08dockerompose-web   Built                                                                                                                                                                                         0.0s
 ✔ Container flask_db   Running                                                                                                                                                                                       0.0s
 ✔ Container flask_app  Started                                                                                                                                                                                       0.3s


Hello from Flask & Postgres!
```

Hello from Flask & Postgres!
```

## Homework Assignment 2: Docker build automation (github action)
```
08.Docker.Docker-compose
 ├──.github/
 │    └──workflows/
 │        └──docker-build.yml
 └──HA2/
     ├── requirements.txt
     ├── Dockerfile
     ├── app.py
     └── docker-compose.yml
```

Slack has a limit of 10 apps per workspace. md-sa-33-25 already has 12 apps. You can only add a workspace with an active subscription.
A decision has been made to send notifications to Telegram.
Actions secrets were used for automation.

__Input__
```
docker build -t flask-app .
```
__Output__

```
[+] Building 10.4s (12/12) FINISHED                                                                                                                                                                                           docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                                                                    0.0s
 => => transferring dockerfile: 368B                                                                                                                                                                                                    0.0s
 => [internal] load metadata for docker.io/library/python:3.11-slim                                                                                                                                                                     0.9s
 => [internal] load .dockerignore                                                                                                                                                                                                       0.0s
 => => transferring context: 2B                                                                                                                                                                                                         0.0s
 => [internal] load build context                                                                                                                                                                                                       0.0s
 => => transferring context: 824B                                                                                                                                                                                                       0.0s
 => [builder 1/5] FROM docker.io/library/python:3.11-slim@sha256:8eb5fc663972b871c528fef04be4eaa9ab8ab4539a5316c4b8c133771214a617                                                                                                       0.0s
 => CACHED [builder 2/5] WORKDIR /app                                                                                                                                                                                                   0.0s
 => [builder 3/5] COPY requirements.txt .                                                                                                                                                                                               0.2s
 => [builder 4/5] RUN pip install --prefix=/install -r requirements.txt                                                                                                                                                                 6.6s
 => [builder 5/5] COPY . .                                                                                                                                                                                                              0.8s
 => [stage-1 3/4] COPY --from=builder /install /usr/local                                                                                                                                                                               0.5s
 => [stage-1 4/4] COPY . .                                                                                                                                                                                                              0.3s
 => exporting to image                                                                                                                                                                                                                  0.2s
 => => exporting layers                                                                                                                                                                                                                 0.1s
 => => writing image sha256:afe02896d83b08e8911cb2afbc6b6cd8a139ebf7fd35bbb08cfb0dc463adb60c                                                                                                                                            0.1s
 => => naming to docker.io/library/flask-app                    
 ```

 __Input__
 ```
 docker run -d -p 5000:5000 --name flask_app flask-app
 git commit -m "Add README.md"
 git push origin md-sa-33-25
 ```
