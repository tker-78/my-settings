# SSH接続での公開

UbuntuマシンにiOSなどのクライアントからssh接続できるようにする。

```
$ sudo apt install openssh-server
$ sudo apt install ufw
$ sudo systemctl enable --now ssh
$ sudo ufw allow 22/tcp
```