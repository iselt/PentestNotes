# PHP 伪协议

## 什么是伪协议

- 伪协议是 PHP 中的一种特殊的语法，用于访问各种资源，如文件、网络、数据库等。
- 伪协议的格式为：`协议名：//参数`，其中协议名是指定的，参数是根据不同的协议而不同的。
- 伪协议的使用方法有
  - `file_get_contents("伪协议：//参数")`
  - `include("伪协议：//参数")`
  - `require("伪协议：//参数")`

## 常见的伪协议

### file://

- "file://"协议用于读取本地文件，其参数为文件的路径。
- 例如：`file:///etc/passwd`，表示读取本地的/etc/passwd 文件。

### http://

- "http://"协议用于读取远程文件，其参数为远程文件的 URL。
- 例如：`http://www.baidu.com`，表示读取百度的首页。

### php://

- "php://"协议用于读取 PHP 的输入和输出流，其参数为输入输出流的类型。
- 例如：`php://input`，表示读取 PHP 的输入流；`php://output`，表示读取 PHP 的输出流。
- 例如：`php://filter/read=convert.base64-encode/resource=/etc/passwd`，表示读取/etc/passwd 文件的 base64 编码。
- file_get_contents() 支持 php://input，可以

### zip://

- "zip://"协议用于读取 ZIP 压缩文件中的文件，其参数为 ZIP 压缩文件的路径。
- 例如：`zip://test.zip#test.txt`，表示读取 test.zip 压缩文件中的 test.txt 文件。

### phar://

- "phar://"协议用于读取 PHAR 压缩文件中的文件，其参数为 PHAR 压缩文件的路径。
- 例如：`phar://test.phar/test.txt`，表示读取 test.phar 压缩文件中的 test.txt 文件。

### data://（php 5.2.0 起）

- "data://"协议用于读取数据，其参数为数据的类型。
- 例如：`data://text/plain;base64,SGVsbG8sIFdvcmxkIQ==`，读取 base64 编码的字符串，返回解码后的值。
