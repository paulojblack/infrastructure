# Dockerfile

A quick glance reveals this Dockerfile as wildly insecure, do not use it for anything meaningful. This image is generated for ephemeral local development, initially nginx config.

`docker build . -t pauloblack/dev-ubuntu`
`docker run -p 3000:3000 -it pauloblack/dev-ubuntu /bin/bash`