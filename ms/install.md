# install lxdmosaic
- after update
```lxd init```

```lxc launch ubuntu:20.04 lxdMosaic```

```lxc exec lxdMosaic bash```

```curl https://raw.githubusercontent.com/turtle0x1/LxdMosaic/master/examples/install_with_clone.sh >> installLxdMosaic.sh```

```chmod +x installLxdMosaic.s```

```./installLxdMosaic.sh```

- return host

```lxc config device add lxdMosaic port443 proxy listen=tcp:0.0.0.0:10443 connect=tcp:127.0.0.1:443```

# docker in lxc
- set option
```bash
lxc config set docker-host security.privileged true
lxc config set docker-host security.nesting true
```

```apt update && apt upgrade -y && apt install docker.io && docker run hello-world```

# install gossa(file browser)
```wget https://github.com/pldubouilh/gossa/releases/download/v0.2.0/gossa-linux-x64```

```mv gossa-linux-x64 /usr/local/bin/gossa```

```chmod a+x /usr/local/bin/gossa```

## This page was created based on this
[https://gihyo.jp/admin/serial/01/ubuntu-recipe/0636?page=1](https://takuya-1st.hatenablog.jp/entry/2020/09/12/010000)

[https://takuya-1st.hatenablog.jp/entry/2020/09/12/010000](https://takuya-1st.hatenablog.jp/entry/2020/09/12/010000)
