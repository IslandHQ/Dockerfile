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

## This page was created based on this
[https://gihyo.jp/admin/serial/01/ubuntu-recipe/0636?page=1]()
