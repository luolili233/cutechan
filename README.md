# cutechan [![Build Status](https://travis-ci.org/cutechan/cutechan.svg?branch=master)](https://travis-ci.org/cutechan/cutechan)

K-pop oriented imageboard started as [meguca](https://github.com/bakape/meguca) fork.

## Quick Start with Docker Compose

The easiest way to run cutechan is using Docker Compose:

```bash
# Build and start all services
docker-compose up -d

# Or build first, then start
docker-compose build
docker-compose up -d

# Check status
docker-compose ps

# View logs
docker-compose logs cutechan
```

Then open <http://localhost:8001> in your browser.

## Build

To build the project from source:

```bash
# Build with Docker Compose (recommended)
docker-compose build

# Or build production Docker image directly
docker build -t cutechan .

# Or build development image
docker build -f Dockerfile-dev -t amd64/cutechan-dev .
```

## Development Setup

For development, you can use the dev container:

```bash
# Build dev image
docker build -f Dockerfile-dev -t amd64/cutechan-dev .

# Run dev container
docker run -it --rm --name cutechan-dev -p 127.0.0.1:8001:8001 \
  -v ./pgdata:/var/lib/postgresql -v $PWD:/cutechan amd64/cutechan-dev
```

### Database Setup (in dev container)

```bash
# Recreate cluster on first run
pg_dropcluster --stop 16 main
pg_createcluster --start 16 main

# Run DB server after container start
/etc/init.d/postgresql start
```

### Build (inside dev container)

```bash
# Build everything
make

# Or build separately
make client    # Build client-side assets
make server    # Build server binaries

# Watch mode for development
make client-watch
```

### Setup

- `make server-config` to init config
- `make server-db` to init database
- `make serve` and open <http://localhost:8001> in a browser
- Login into the `admin` account with the password `password`
- Change the default password
- Create a board from the administration panel
- Configure server from the administration panel

## License

[AGPLv3+](LICENSE).
