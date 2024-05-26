
# Projects Build Process Documentation

## Dotnet Build Process Documentation:---

### Command: `dotnet build --configuration Release`
* **Purpose:** Compiles the code in release mode, optimizing it for performance.
* **Explanation:** This command compiles the code in the specified configuration (Release in this case), which typically includes optimizations for performance. However, it does not prepare the application for deployment.

### Command: `dotnet publish -c Release -o published`
* **Purpose:** Prepares the application for deployment.
* **Explanation:** Similar to the previous command, this compiles the code in release mode. However, it goes further by preparing the application for deployment. The `-o` flag specifies the output directory where the published application will be placed.

### SCP Command: `scp -i key.pem -r published/* ubuntu@13.212.146.171:/published-docker`
* **Purpose:** Transfers the built Next.js application to a remote server.
* **Explanation:** Copies the contents of the nextjs-dockerapp directory to a specified directory on a remote server using Secure Copy Protocol (SCP).

### After Entry on the server:

```bash
sudo apt-get update && \
sudo apt-get install -y dotnet-sdk-8.0

sudo apt-get update && \
sudo apt-get install -y aspnetcore-runtime-8.0

sudo apt-get install -y dotnet-runtime-8.0

sudo apt install zlib1g

cd published-docker

dotnet published\learn-dotnet.dll
```

### Automated Build Process:

```
docker build -t dontnet-app.

docker tag dotnet-app shafikur/dotnet-app

docker push shafikur/dotnet-app
```

#### Additional Note

* Project Management: Push your project to GitHub for version control and 
  collaboration.
* CI/CD: Consider integrating this build process into a CI/CD pipeline for
  automated testing and deployment.





# Nextjs Build Process Documentation (Manual and Auto):---

## Manual Build Process

### Command: `npm run build`
* **Purpose:** Build the Next.js application.
* **Explanation:** Executes the build script defined in the `package.json` file, generating a production-ready build of the Next.js application.

### SCP Command: `scp -i key.pem -r nextjs-dockerapp/* ubuntu@13.212.146.171:/nextjs-docker`
* **Purpose:** Transfers the built Next.js application to a remote server.
* **Explanation:** Copies the contents of the `nextjs-dockerapp` directory to a specified directory on a remote server using Secure Copy Protocol (SCP).

### After Entry on the server:

```bash
# Node.js Installation

curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash - &&\
sudo apt-get install -y nodejs

cd nextjs-docker

sudo apt install npm -y

npm i

npm run start

```

## Automated Build Process:---

```
docker build -t nextjs-app .

docker tag nextjs-app shafikur/nextjs-app

docker push shafikur/nextjs-app
```


#### Additional Note:

* Project Management: Push your project to GitHub for version control and 
  collaboration.
* CI/CD: Consider integrating this build process into a CI/CD pipeline for
  automated testing and deployment.