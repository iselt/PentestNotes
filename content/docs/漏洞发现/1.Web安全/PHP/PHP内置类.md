# PHP 内置类

## SplFileObject

与伪协议结合，可用于读取文件内容。

```php
<?php
$file = new SplFileObject('php://filter/read=convert.base64-encode/resource=/etc/passwd');
echo $file->fread($file->getSize());
?>
```
