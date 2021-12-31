FROM ubuntu

RUN apt-get update;
RUN apt-get install -yq sudo iputils-ping vim

### NGINX

RUN apt install -yq curl gnupg2 ca-certificates lsb-release ubuntu-keyring;
RUN curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor | tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null; \
    echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
    | tee /etc/apt/sources.list.d/nginx.list; \
    echo "Package: *\nPin: origin nginx.org\nPin: release o=nginx\nPin-Priority: 900\n" \
    | tee /etc/apt/preferences.d/99nginx; \
    DEBIAN_FRONTEND="noninteractive" apt install -yq nginx;
    

RUN mkdir -p /data/www;
COPY ./index.html /data/www/
COPY ./nginx.conf /etc/nginx/nginx.conf

# Set root password to root
RUN echo "root:root" | chpasswd

# Add pblack superuser
RUN useradd -rm -d /home/pblack -s /bin/bash -g root -G sudo -u 1001 pblack
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN echo 'pblack:pblack' | chpasswd
# USER pblack
# WORKDIR /home/pblack

EXPOSE 3000

