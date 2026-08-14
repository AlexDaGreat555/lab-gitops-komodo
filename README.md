# Git-backed Deployments with Komodo

This repository is the starter for Lab 4. Open it in the provided devcontainer
and follow the tasks on the course website.

The devcontainer starts a local Komodo 2.3.0 Core, MongoDB, and Periphery. No
cloud account or infrastructure credentials are required. Both Komodo and the
lab service use the Docker daemon attached to the devcontainer.

## Local Komodo

The web interface is available at <http://localhost:9120>.

```text
username: lab-admin
password: lab04-local-only
```

These credentials protect only the disposable, local lab instance. They are
intentionally committed in `.env.lab` so every student receives the same
environment.

If Komodo is not running, start it with:

```console
./scripts/start-komodo
```

## Supplied service images

Use these complete `linux/amd64` image references. The digest selects a single
platform-specific image manifest rather than a multi-platform index.

Version 1:

```text
python:3.13.7-alpine3.22@sha256:527c28b29498575b851ad88e7522ac7201bbd9e920d2c11b00ff2b39b315f5f8
```

Version 2:

```text
python:3.13.8-alpine3.22@sha256:d74ca7409552835ab7517738e9248d8995ad7c42cba30f3278eb3ee120957d3d
```

The Compose file contains the deliberately small HTTP service used by both
images. Each image has a different baked `PYTHON_VERSION`, which the service
maps to the fixed `/version` response for that lab version. Students change
only the image reference.

## Commands

Establish the expected failing baseline before editing the declarations:

```console
./scripts/check-lab
```

After replacing both starter placeholders and pushing the declarations to your
fork, import the Stack:

```console
./scripts/import-stack lab04/stack.toml
```

After deploying through Komodo, verify the reported version:

```console
./scripts/smoke-test 'lab04 version 1'
./scripts/smoke-test 'lab04 version 2'
```

The final checker expects the version 2 image and removes any service container
that it created itself. It leaves an already-running Komodo deployment in
place.
