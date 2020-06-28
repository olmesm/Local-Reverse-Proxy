# Local Reverse Proxy

Mock <http://google.com> using nginx as a reverse proxy to a locally running webserver.

Used for local testing of DNS resolving, and routing. Particularly useful for CMS migrations.

## Requires

- [SwitchHosts]
- [Docker]
- [nvm], node, or a webserver of your choice.

## Setup

As a proof of working this is intended for mac setup only. This is replicatable, but untested for other platforms.

```bash
# Install switchhosts
brew cask install switchhosts
```

Add the following to switchhosts > preferences > Commands

```bash
sudo -S killall -HUP mDNSResponder
```

Create a new workspace "local-proxys" with the `+`

Add the following and then activate

```txt
127.0.0.1 google.com
```

In an additional terminal session

```bash
mkdir tmp

# Make an index.html file for serving
echo "this is not google" > tmp/index.html

# Serve the folder using a node webserver
npx serve tmp
```

Ensure the port used by the `npx serve` process is the same as the port set in the [proxy_pass](conf/web.conf) (most likely 5000)

**Note** We're not using `https` for this

```bash
docker-compose up
```

Navigate <http://google.com>

<!-- MARKDOWN REFS -->

[switchhosts]: https://github.com/oldj/SwitchHosts
[docker]: https://www.docker.com/
[nvm]: https://github.com/nvm-sh/nvm
