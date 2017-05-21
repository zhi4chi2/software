发任意邮件至 GreenDiZhi@gmail.com 可以获得最新网址

# bug

密码不能有特殊字符，应使用 simple 密码策略，否则登录不了。

# Reference

- https://www.greenjsq.me/shiyong/88.html - 测试不成功
- https://www.greenjsq.me/user-xianlu.html
- https://www.greenjsq.me/shiyong/67.html - 最后不应该使用 ca.crt 而是使用默认的与连接名同名的 pem 文件才成功。例如 /home/me/.cert/nm-openvpn/UnitedStates-05-ca.pem