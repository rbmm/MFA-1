# MFA-1
 
configuration:

Domain: RBMM ( DNS=RBMM.local ), Forest=RBMM.local
DC,KDC: rbmmserver ( run here) (full name rbmmserver.TPM11.RBMM.local )
joined comp: TPM11 (full name TPM11.RBMM.local)

domain user: Harry@RBMM.local (not admin, but in Remote Desktop Users group )

NLA - enabled

root cert - root.cer
kdc cert - kdc.cer (signed by root.cer)
harry cert - harry.cer (signed by root.cer)

#1 login from standalone workstation - [![Watch the video]](https://www.youtube.com/watch?v=JjRSo4DP5Ik)
#2 login from another domain - [![Watch the video]](https://www.youtube.com/watch?v=uV36VbMKX6c)

in case not domain join comp need:
1.) install domain root cert in local comp trusted root
2.) set 
  Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\RBMM.local
    KdcNames REG_MULTI_SZ rbmmServer.RBMM.local
3.) edit hosts file for add ip for rbmmServer.RBMM.local and TPM11.RBMM.local


==============================================================================================================

IVSCR.exe need run on DC
it create GPO ( Rbmm GPO ) for install inside domain
in %LOCALAPPDATA%\Rbmm USC "RbmmMFA.bat" and "RbmmMFA.exe"
for install on not domain join comp - need run "RbmmMFA.bat" 

certificate for user (in domain) auto enroled on first login/unlock/run as local (not in case rdp logon)
or can be created/revoked from admin tool (inside Control Panel\All Control Panel Items\Windows Tools )
uninstall from Control Panel\Programs\Programs and Features or from Settings > Apps > Installed Apps
logs in %windir%\temp\CDABA566C6BB44b7BFF0BF8D47553C1F\ 
