## Install docker on VM (Debian)

### Setup repository

1. Update the `apt` package index and install packages to allow apt to use a repository over HTTPS:

```
$ sudo apt-get update
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

2. Add Docker’s official GPG key:

```
 $ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg 
```

3. Use the following command to set up the **stable** repository. To add the `nightly` or `test` repository, add the word nightly or test (or both) after the word `stable` in the commands below. Learn about nightly and test channels.

```
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install Docker Engine

This procedure works for Debian on `x86_64` / `amd64`, `armhf`, `arm64`, and `Raspbian`.

```
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## Install Compose on Linux Systems

On Linux, you can download the Docker Compose binary from the Compose repository release page on GitHub. Follow the instructions from the link, which involve running the curl command in your terminal to download the binaries. These step-by-step instructions are also included below.

1. Run this command to download the current stable release of Docker Compose:

```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

2. Apply executable permissions to the binary:

```
$ sudo chmod +x /usr/local/bin/docker-compose
```

3. Test the installation.

```
$ docker-compose --version
```

## Running services

### Run Traefik

```
$ docker-compose -f docker-compose.traefik.yml up -d
```

### Run our service

To run our service, we will need to create a `.env` file to set default values, like:

```
# .env

URL=myurl.com
EMAIL=myemail@gmail.com
```
So we can run with:

```
docker-compose -f docker-compose.yml up -d
```