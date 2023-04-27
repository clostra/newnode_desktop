Desktop (MacOS/Linux) client for NewNode VPN.   Usable by altrustic nodes and as a local http/https proxy.

To use this as a local proxy, define the following environment variables in `$HOME/.profile` or (if bash is your shell)`$HOME/.bashrc`:
```bash
export http_proxy=http://localhost:8006
export https_proxy=http://localhost:8006
```

Then source whichever file those variables are defined in.
```bash
. $HOME/.bashrc
```

Then start or restart your web browser or other client.
