# 设置 .html 打开的默认程序
360 会使得在【控制面板\所有控制面板项\默认程序\设置默认程序】中更改默认程序无效。原因是注册表键只有读取权限。


修正： HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\FileExts\.html\UserChoice 右键【权限】，使当前用户有完全控制的权限，而不是只能读取。然后再在【控制面板\所有控制面板项\默认程序\设置默认程序】中修改。
