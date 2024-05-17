---

title: How to Use a Docker Image with Pre-installed Sui Binaries?

---

Step 1: Install [Docker](https://docs.docker.com/get-docker/):  you need to install Docker on your machine. Docker can be installed on a variety of systems, including Windows, MacOS, and various distributions of Linux.

Step 2: Pull the [Official Sui](https://hub.docker.com/r/mysten/sui-tools/tags) Docker image. The Official Sui Docker image can be found [here](https://hub.docker.com/r/mysten/sui-tools/tags).

By following these steps, you will have successfully set up a Docker image with pre-installed Sui binaries, ready to be utilized for your projects.

```
docker pull mysten/sui-tools:testnet
```

Step 3: Start and shell into the Docker container
```
docker run --name suidevcontainer -itd mysten/sui-tools:testnet

docker exec -it suidevcontainer bash
```