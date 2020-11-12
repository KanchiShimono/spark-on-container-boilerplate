# Docker Compose

Docker Compose for Spark cluster with Jupyter Lab

## Usage

You can choose two way to access cluster by Jupyter Lab or Visual Studio Code.

### Jupyter Lab

Creating cluster.

```sh
docker-compose up -d
```

Then access Jupyter Lab `http://localhost:8888`.

### Visual Studio Code

Open this directory.

```sh
code .
```

Then open command palette.

- Mac: `command + shift + P`
- Windows: `ctrl + shift + P`

Select `Remote-Containers: Open Folder in Container...` and open `docker_compose` directory in explorer.

## Services

| Name           | Role                                                                                                      |
| -------------- | --------------------------------------------------------------------------------------------------------- |
| jupyter        | Jupyter Lab container. Assuemed to be used as workspace. Visual Studio Code also attaches this container. |
| master         | Spark master node.                                                                                        |
| worker         | Spark worker node.                                                                                        |
| history-server | History server for monitoring previous spark jobs.                                                        |
