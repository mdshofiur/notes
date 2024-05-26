# Manual and Automatic Deploy Process Documentation

## Manual Deploy Process

### For Dotnet

#### SCP Command: 
```bash
scp -i key.pem -r nextjs-dockerapp/* ubuntu@13.212.146.171:/nextjs-docker

sudo apt update -y

sudo apt install unzip -y

sudo unzip learn-dotnet.zip

sudo dotnet published\learn-dotnet.dllj
```

### For NEXTJS

```
scp -i key.pem -r nextjs-dockerapp/* ubuntu@13.212.146.171:/nextjs-docker

sudo apt update -y

sudo apt install unzip -y

sudo unzip nextjs-app.zip

npm run start
```

## ------ Automatic Deploy Process-------

```

sudo apt update -y

sudo apt install docker.io docker-compose -y


* FOR DOTNET

docker pull shafikur/dotnet-app

docker run -p 5000:8080 --name dotnet-container dontnet-app


* FOR NEXTJS

docker pull shafikur/nextjs-app

docker run -p 4000:80 --name nextjs-container nextjs-app
```
