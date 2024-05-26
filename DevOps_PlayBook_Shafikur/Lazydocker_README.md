# To install LazyDocker, follow these steps:


1. Clone the LazyDocker repository:

```bash
git clone https://github.com/jesseduffield/lazydocker.git
cd lazydocker

docker build -t lazyteam/lazydocker \
    --build-arg BUILD_DATE=`date -u +"%Y-%m-%dT%H:%M:%SZ"` \
    --build-arg VCS_REF=`git rev-parse --short HEAD` \
    --build-arg VERSION=`git describe --abbrev=0 --tag`
```

2. Add an alias for LazyDocker:
```
echo "alias lzd='lazydocker'" >> ~/.zshrc

```

3. 

```
lazydocker

```
