## 树莓派设置 WIFI

在 boot 分区新建 `wpa_supplicant.conf` 文件，输入下述内容：

```
country=CN
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
 
network={
    ssid="tjdesktopwifi"
    psk="tjwifi123"
    key_mgmt=WPA-PSK
    priority=1
}
 
network={
    ssid="Xiaomi_CBA3"
    psk="tjmiwifi123"
    key_mgmt=WPA-PSK
    priority=2
}
```

## 树莓派开启 ssh

在 boot 分区创建一个名称为 `ssh` 的空文件即可。

可以先通过 ssh 密码登录的方式连接树莓派，账号: **pi**，密码: **raspberry** 。

然后再开启 ssh 密钥登录：

```shell
pi@raspberrypi:~ $ mkdir .ssh && cd .ssh
pi@raspberrypi:~/.ssh $ vi id_rsa.pub
```

在 `id_rsa.pub` 文件里放入 ssh 连接客户端的公钥，如下所示：

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCXE+pQP3NJ/poHwBgS4l99t1GfKi9OEqOjYHojirfZEMzRato6t9CXR9jX/NWoNevZ5/a6tlnHCdGZWT7JDA05GQ8FeI8RbkQM0Ecg6HVxybBp7KW6Lh9yKAgjs4dRUQik9q5JwQygERIbsVL8OVPKSW1vmMBzbu2x/fiu1Bkbxm+cIGT4hSTBuzZRuVzZkK4NZOUFqp9GZv3ufJ5TEfiuTjHiYOo6lSpQGgt/jvBbTJ4MoNUjKUHqTnRSvx4XizX+2z7YPODgOywD1dfofzkFx2ztM8NsZAxvqqXxPSKc5RPi+q7SheTSVj9S6WrR98g6CO8VML8TPskAK/L1T2AGV/tKDw1PVkrjbCq1vU4kPNM2Agq7DJ4Cf3lLplcKFle6DcHxo5kFb0IJQakJ2SivPDv6AGUyKWByAKy3139OGxTPrLE7+OhfzlacX6Pe99JZpvfDY8dh31ekQwrsSlKVLk6bwJ/PW8DMZQd5T1o8KYCy09ifGJdMgbz0YByBJos= tangjia.jackis@qq.com
```

然后在输入：

```shell
pi@raspberrypi:~/.ssh $ cat id_rsa.pub >> authorized_keys
pi@raspberrypi:~/.ssh $ sudo /etc/init.d/ssh restart
```

这样即可正常通过**密钥 ssh** 连接树莓派了。