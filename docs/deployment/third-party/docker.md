# Run nio in a <span class="allow-caps">Docker</span> container

Running the nio Platform as a [Docker](https://docker.com) container offers several benefits such as better deployment and lifecycle management. However, niolabs does not currently have a public downloadable Docker image because different plans often have different nio binaries. Instead, you can build and manage your own Docker image using your nio binary.

---
## Clone the repository

To build a Docker image, start by cloning the [nio-docker repository](https://github.com/niolabs/nio-docker).

```
git clone https://github.com/niolabs/nio-docker.git nio-docker
cd nio-docker
```

Then add a submodule for the default project
```
git submodule add https://github.com/niolabs/project_template.git default_project
```

---
## Configure the Project

Before running nio, the `nio.conf` file of the project will need to be configured for Pubkeeper communication. If you are using a nio-hosted Pubkeeper server, obtain your hostname and token from the [System Designer](http://app.n.io/design) in the edit modal for your system as explained here: [docs.n.io/running-nio/in-the-cloud.html#pk-credentials](/quickstart#pk-credentials).

1. Open `default_project/nio.conf`.
2. Under the `user_defined` section, copy your Pubkeeper hostname and token to `PK_HOST` and `PK_TOKEN`.
3. For `WS_HOST`, copy your Pubkeeper hostname, but replace `pubkeeper` with `websocket`.

---
## Creating a <span class="allow-caps">Docker</span> image

Once you have downloaded your binary from the [binary downloads page](https://account.n.io/binaries/download), you can build a corresponding Docker image from that binary.

1. Copy your wheel file into the directory.
```
cp your-wheel-file.whl nio-docker
```

2. Build the Docker image by passing the name of the wheel file as the `WHEEL_FILE` build argument (the `X`s represent the date of the binary in YYYYMMDD format):
```
docker build -t my-binary-image:latest --build-arg WHEEL_FILE=nio_full-XXXXXXXX-py3-none-any.whl .
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
