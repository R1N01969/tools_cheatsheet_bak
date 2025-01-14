```sh
# コンテナID確認
sudo docker ps

# 自動起動確認
# inspectの引数にコンテナIDのを指定
sudo docker inspect 0a72713635de --format='{{.HostConfig.RestartPolicy.Name}}'
# always
```

| ステータス          | 状態                       |
| -------------- | ------------------------ |
| always         | 自動起動が有効                  |
| unless-stopped | 自動起動が有効（手動停止されたら自動起動しない） |
| no             | 自動起動が無効                  |

```sh
# 自動起動停止
sudo docker update --restart no 0a72713635de
```