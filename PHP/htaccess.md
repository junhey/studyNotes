> .htaccess设置

---
title: 301跳转
---

单页面：

```
Redirect 301 /oldpage.html http://www.yoursite.com/newpage.html
Redirect 301 /oldpage2.html http://www.yoursite.com/folder/
```

整站：

```
Redirect 301 / http://newsite.com/
```
---
title: 自动添加文件
---

```
php_value auto_prepend_file "/real/path/to/file/functions.php"
php_value auto_append_file "/real/path/to/file/footer.php"
```
---
title: 自定义错误页面
---

```
ErrorDocument 400 /400.html
ErrorDocument 401 /401.html
ErrorDocument 403 /403.html
ErrorDocument 404 /404.html
ErrorDocument 405 /405.html
ErrorDocument 408 /408.html
ErrorDocument 414 /414.html
ErrorDocument 500 /500.html
ErrorDocument 502 /502.html
ErrorDocument 504 /504.html
```
---
title: 允许或者进制访问
---

允许某 IP 访问

```
Order deny,allow
Deny from All
Allow from xxx.xxx.xxx.xxx
Allow from xxx.xxx.xxx.xxy
```

禁止某特定 IP 访问

```
Order deny,allow
Allow from All
Deny from xxx.xxx.xxx.xxx
Deny from xxx.xxx.xxx.xxy
```
---
title: 设置 index 页面
---

```
DirectoryIndex index2.html
```
---
title: 强制为 XHTML 类型
---

```
RewriteEngine On
RewriteCond %{HTTP_ACCEPT} application/xhtml\+xml
RewriteCond %{HTTP_ACCEPT} !application/xhtml\+xml\s*;\s*q=0
RewriteCond %{REQUEST_URI} \.html$
RewriteCond %{THE_REQUEST} HTTP/1\.1
RewriteRule .* - "[T=application/xhtml+xml; charset=ISO-8859-1]"
```
---
title: 让 favicon 走正确路线
---

```
# REDIRECT FAVICON.ICO
<ifmodule mod_rewrite.c>
RewriteCond %{REQUEST_URI} !^/favicon\.ico [NC]
RewriteCond %{REQUEST_URI} favicon\.ico    [NC]
RewriteRule (.*) http://css-tricks.com/favicon.ico [R=301,L]
</ifmodule>
```

```
# REDIRECT AJAX-LOADER
<ifmodule mod_rewrite.c>
RewriteCond %{REQUEST_URI} !^/images/ajax\-loader\.gif [NC]
RewriteCond %{REQUEST_URI} ajax\-loader\.gif           [NC]
RewriteRule (.*) http://css-tricks.com/images/ajax-loader.gif [R=301,L]
</ifmodule>
```
---
title: 强制让文件打开时下载
---

```
AddType application/octet-stream .csv
AddType application/octet-stream .xls
AddType application/octet-stream .doc
AddType application/octet-stream .avi
AddType application/octet-stream .mpg
AddType application/octet-stream .mov
AddType application/octet-stream .pdf
```
---
title: 强制 https
---

```
RewriteEngine on
RewriteCond %{HTTPS} !on
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```

```
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
```
---
title: Gzip 压缩
---

```
# BEGIN GZIP
<ifmodule mod_deflate.c>
AddOutputFilterByType DEFLATE text/text text/html text/plain text/xml text/css application/x-javascript application/javascript
</ifmodule>
# END GZIP
```

```
<IfModule mod_filter.c>
    AddOutputFilterByType DEFLATE "application/atom+xml" \
                                  "application/javascript" \
                                  "application/json" \
                                  "application/ld+json" \
                                  "application/manifest+json" \
                                  "application/rdf+xml" \
                                  "application/rss+xml" \
                                  "application/schema+json" \
                                  "application/vnd.geo+json" \
                                  "application/vnd.ms-fontobject" \
                                  "application/x-font-ttf" \
                                  "application/x-javascript" \
                                  "application/x-web-app-manifest+json" \
                                  "application/xhtml+xml" \
                                  "application/xml" \
                                  "font/eot" \
                                  "font/opentype" \
                                  "image/bmp" \
                                  "image/svg+xml" \
                                  "image/vnd.microsoft.icon" \
                                  "image/x-icon" \
                                  "text/cache-manifest" \
                                  "text/css" \
                                  "text/html" \
                                  "text/javascript" \
                                  "text/plain" \
                                  "text/vcard" \
                                  "text/vnd.rim.location.xloc" \
                                  "text/vtt" \
                                  "text/x-component" \
                                  "text/x-cross-domain-policy" \
                                  "text/xml"

</IfModule>
```
---
title: 文件夹密码访问
---

```
AuthType Basic
AuthName "This Area is Password Protected"
AuthUserFile /full/path/to/.htpasswd
Require valid-user
```

[Reference](https://css-tricks.com/snippets/htaccess/password-protect-folders/)
---
title: 设置过期时间
---

```
# BEGIN EXPIRES
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresDefault "access plus 10 days"
    ExpiresByType text/css "access plus 1 week"
    ExpiresByType text/plain "access plus 1 month"
    ExpiresByType image/gif "access plus 1 month"
    ExpiresByType image/png "access plus 1 month"
    ExpiresByType image/jpeg "access plus 1 month"
    ExpiresByType application/x-javascript "access plus 1 month"
    ExpiresByType application/javascript "access plus 1 week"
    ExpiresByType application/x-icon "access plus 1 year"
</IfModule>
# END EXPIRES
```
---
title: 网址添加 www 或者删除 www
---

强制添加 www：

```
RewriteEngine On
RewriteCond %{HTTP_HOST} ^your-site.com [NC]
RewriteRule ^(.*)$ http://www.your-site.com/$1 [L,R=301]
```

强制去除 www：

```
RewriteEngine On
RewriteCond %{HTTP_HOST} !^your-site.com$ [NC]
RewriteRule ^(.*)$ http://your-site.com/$1 [L,R=301]
```
