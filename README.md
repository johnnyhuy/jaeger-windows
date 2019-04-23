# Jaeger for Windows

This is a repository with Jaeger pull servers in Windows Docker containers.

## Usage

Run the following command to get this container running! There is also support for previous Windows versions.

```bash
# Windows Server 1809
docker run --rm \
    -p 5775:5775/udp \
    -p 6831:6831/udp \
    -p 6832:6832/udp \
    -p 5778:5778 \
    -p 16686:16686 \
    -p 14268:14268 \
    -p 9411:9411 \
    johnnyhuy/jaeger-windows:latest

# OR

# Windows Server 1803
docker run --rm \
    -p 5775:5775/udp \
    -p 6831:6831/udp \
    -p 6832:6832/udp \
    -p 5778:5778 \
    -p 16686:16686 \
    -p 14268:14268 \
    -p 9411:9411 \
    johnnyhuy/jaeger-windows:1803

# OR

# Windows Server 2016
docker run --rm \
    -p 5775:5775/udp \
    -p 6831:6831/udp \
    -p 6832:6832/udp \
    -p 5778:5778 \
    -p 16686:16686 \
    -p 14268:14268 \
    -p 9411:9411 \
    johnnyhuy/jaeger-windows:win2016
```

## Prerequisites

- Docker & Windows (duhh!)

## Contribution

- **Johnny Huynh** - Initial changes in this repository

## License

This project is licensed under the MIT license, see [LICENSE](https://github.com/johnnyhuy/grafana-windows/blob/master/LICENSE) for more information.
