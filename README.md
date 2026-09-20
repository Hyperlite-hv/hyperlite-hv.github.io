# Hyperlite APT repository

Replace `<repository-url>` with the address where this directory is served
(the public mirror is `https://twikles.github.io/hyperlite`).

```bash
curl -fsSL <repository-url>/hyperlite-archive-keyring.asc | gpg --dearmor -o /usr/share/keyrings/hyperlite-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hyperlite-archive-keyring.gpg] <repository-url> stable main" > /etc/apt/sources.list.d/hyperlite.list
apt update && apt install hyperlite
```

Note on GitHub Pages: it is a multi-node CDN without strong consistency between
files published in the same commit, so InRelease and Packages can be served out
of sync for a while (`apt update` then fails with "File has unexpected size").
Serving this directory from a single origin (for example nginx, see
installer/hyperlite-apt-repo.nginx.conf) avoids the problem.
