<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/Mad-Pixels/.github/raw/main/profile/banner.png">
  <source media="(prefers-color-scheme: light)" srcset="https://github.com/Mad-Pixels/.github/raw/main/profile/banner.png">
  <img alt="MadPixels" src="https://github.com/Mad-Pixels/.github/raw/main/profile/banner.png">
</picture>

![CI](https://github.com/Mad-Pixels/images/workflows/Main%20commit/badge.svg)
![License](https://img.shields.io/github/license/Mad-Pixels/images)

# Docker Images Repository
Central repo for building and publishing all Mad-Pixels Docker images.  
#### Available images: [ghcr.io/mad-pixels](https://github.com/orgs/Mad-Pixels/packages)

## Quickstart
Pull and run any image by name:
```bash
docker pull ghcr.io/mad-pixels/images/<image-name>:<tag> or latest
docker run --rm -it ghcr.io/mad-pixels/images/<image-name>:<tag> or latest 
```

## Adding a New Image
#### 1. Create directory under `images/`:
```bash
mkdir images/myapp
```

#### 2. Add a `Taskfile` entry:
```bash
myapp:
  desc: Build myapp image.
  vars:
    VERSION: v1.0.0   # or dynamic lookup via GitHub API, etc.
  cmds:
    - task: _docker/buildx
      vars:
        CONTEXT: "{{.base_context}}/{{.TASK_NAME}}"
        TAG:     "{{.VERSION}}"
        BUILD_ARGS: >-
          --build-arg ALPINE_VERSION={{.image_alpine_ver}}
          --build-arg APP_VERSION={{.VERSION}}
```
Available parameters for `vars`:
| Parameter     | Required | Default                          | Description                  |
|---------------|----------|----------------------------------|------------------------------|
| `TAG`         | ✅       | -                                | Image tag                    |
| `CONTEXT`     | ✅       | -                                | Path to Dockerfile directory |
| `platforms`   | ❌       | `linux/amd64,linux/arm64`        | Target platforms             |
| `dockerfile`  | ❌       | `{{.CONTEXT}}/Dockerfile`        | Dockerfile path              |
| `context_path`| ❌       | `./{{.CONTEXT}}`                 | Build context                |
| `BUILD_ARGS`  | ❌       | -                                | Docker build arguments       |

#### 3. Commit & push — CI will detect `images/myapp` changed and build that image.

#### 4. Auto-Updates (optional) in `monthly_update.yml`
```yaml
images:
  ...
  - myapp
```

## Contributing
We ❤️ community contributions!

1. Fork → clone
2. Add/modify images/<name> & Taskfile
3. Open PR against main
4. CI will lint & build after merge changes in main branch

## License
© 2025 Mad-Pixels — [Apache-2.0 license](./LICENSE)
