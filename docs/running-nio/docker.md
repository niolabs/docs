# Run nio in a <span class="allow-caps">Docker</span> container

Running the nio Platform as a [Docker](https://docker.com) container offers several benefits such as better deployment and lifecycle management. However, niolabs does not currently have a public downloadable Docker image because different licenses often have different nio binaries. Instead, you can build and manage your own Docker image using your nio binary.

---
## Clone the repository

The repository to help you build a Docker image can be found in the [nio-docker repository](https://github.com/niolabs/nio-docker).

1. Clone the repository.
```
git clone https://github.com/niolabs/nio-docker.git nio-docker
cd nio-docker
```

---
## Configure the Project

Before running nio, the `nio.conf` file of the project will need to be configured for Pubkeeper communication. If you are using a nio hosted Pubkeeper server, obtain your hostname and token from the [System Designer](http://designer.n.io) in the edit modal for your system.

1. Update the submodules for the default project
```
git submodule update --init --recurisve
```
2. Open `default_project/nio.conf`.
3. Copy your Pubkeeper hostname and token in for `PK_HOST` and `PK_TOKEN` under the `user_defined` section.
4. Copy your hostname in for `WS_HOST` under the `user_defined` section being sure to replace `pubkeeper` with `websocket`.

---
## Creating a <span class="allow-caps">Docker</span> image

Once you have downloaded your binary from the [binary downloads page](https://app.n.io/binaries/download), you can build a corresponding Docker image from that binary.

1. copy your wheel file into the directory.
```
cp your-wheel-file.whl nio-docker
```

2. Build the Docker image by passing the name of the wheel file as the `WHEEL_FILE` build argument (the `X`s represent the date of the binary in YYYYMMDD format):
```
docker build -t my-binary-image:latest --build-arg WHEEL_FILE=nio_lite-XXXXXXXX-py3-none-any.whl .
```

---
## Running nio as a <span class="allow-caps">Docker</span> container

Assuming you have built a Docker image from your binary, you can run the image for different nio project configurations.

To run the nio binary with an empty project, just run the image like so:

```
docker run -p 8181:8181 my-binary-image:latest
```

You can also volume mount in an existing project directory on disk like so:

```
docker run -p 8181:8181 -v /path/to/your/project:/nio/project my-binary-image:latest
```
