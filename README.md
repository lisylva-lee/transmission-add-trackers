[English](#English)

Transmission 辅助脚本，自动添加 Tracker 服务器。

## 使用

```sh
$ curl https://raw.githubusercontent.com/qianbinbin/transmission-add-trackers/master/trans-add-trackers.sh -o /path/to/trans-add-trackers.sh
$ chmod +x /path/to/trans-add-trackers.sh
```

编辑脚本，按需修改以下参数：

```sh
# 主机:端口
# 通常无需修改
HOST="localhost:9091"

# 用户名:密码
AUTH="username:password"
```

然后运行即可。

### Systemd

```sh
$ curl https://raw.githubusercontent.com/qianbinbin/transmission-add-trackers/master/transmission-add-trackers.service -o /etc/systemd/system/transmission-add-trackers.service
```

修改 `/etc/systemd/system/transmission-add-trackers.service` 中以下参数：

```sh
# 用户
User=debian-transmission
# 脚本路径
ExecStart=/path/to/trans-add-trackers.sh
```

执行：

```sh
$ systemctl daemon-reload
$ systemctl enable transmission-add-trackers.service # 开机启动
$ systemctl start transmission-add-trackers.service  # 立即启动
$ systemctl status transmission-add-trackers.service # 查看状态
```

## 已知问题

- [不支持 WebSocket Tracker 服务器](https://github.com/transmission/transmission/issues/5509)。
- `transmission-remote` 无法正确获取已添加的 IPv6 Tracker 服务器，导致重复添加时失败。
- 群晖用户`transmission-remote`问题
- 命令找到它的位置
- which transmission-remote
- 然后在脚本中将所有 transmission-remote 替换为完整路径。例如 /usr/bin/transmission-remote
- 检查环境变量： 确保脚本在运行时能够访问 transmission-remote 命令所在的目录。您可以在脚本的开头添加一行，将 PATH 设置为包含 transmission-remote
  所在的目录，例如：
- export PATH=$PATH:/path/to/transmission/bin PS:请用实际的路径替换 /path/to/transmission/bin
- 如不知道安装路径可以使用命令：sudo find / -name transmission-remote

## 感谢

- https://github.com/XIU2/TrackersListCollection

# English

A shell script for Transmission to add trackers automatically.

## Usage

```sh
$ curl https://raw.githubusercontent.com/qianbinbin/transmission-add-trackers/master/trans-add-trackers.sh -o /path/to/trans-add-trackers.sh
$ chmod +x /path/to/trans-add-trackers.sh
```

Change these values in the script:

```sh
# host:port
# Usually no need to change
HOST="localhost:9091"

AUTH="username:password"
```

Then run the script.

### Systemd

```sh
$ curl https://raw.githubusercontent.com/qianbinbin/transmission-add-trackers/master/transmission-add-trackers.service -o /etc/systemd/system/transmission-add-trackers.service
```

Edit `/etc/systemd/system/transmission-add-trackers.service`:

```sh
User=debian-transmission
ExecStart=/path/to/trans-add-trackers.sh
```

Then:

```sh
$ systemctl daemon-reload
$ systemctl enable transmission-add-trackers.service
$ systemctl start transmission-add-trackers.service
$ systemctl status transmission-add-trackers.service
```

## Known issues

- [Doesn't support WebSocket trackers](https://github.com/transmission/transmission/issues/5509).
- Can't retrieve existing IPv6 trackers with `transmission-remote` properly, which will cause errors when adding duplicates.

## Credits

- https://github.com/XIU2/TrackersListCollection
