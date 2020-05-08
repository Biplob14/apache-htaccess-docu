# apache-htaccess-docu  [![Apache|htaccess]

## Apache Web server directory level configuration chontrol by htaccess

You can check if .htaccess file is present or not by [*this*](https://raw.githubusercontent.com/bolt/htaccess_tester/master/htaccess_tester.php) php file.

### Purpose of htaccess

* Page redirection
* Access control
* Content protection
* Hot link prevention
* Cache control
* Server side error handling
* Rewrite url
* Set server time zone

Create .htaccess file in your folder. It would be better to create the file using a text editor in windows.
**Remember**: This commands are case sensitive and should not be tempered unnecessarily.

### Redirect domain

	RewriteEngine On
	Redirect 301 /http:domain-name.extension

This will redirect you to your desired domain in case you changed your previous domain or you want to go user in different path.

### User authentication

	RewriteEngine On
	AuthType Basic
	AuthName "Restricted Content"
	AuthUserFile absolute-path\.htpasswd
	Require valid-user

None without a proper credentials can acces into this path. The creadentials will be written in .htpasswd file. You haveto provide proper or absolute path of .htpasswd file in order to get access credentials.
On .htpasswd file user and password are written as a format-

	user-name:password


### Cache handle

	<FilesMatch "\.(file-ext|file-ext|file-ext|file-ext)$">
		Header set Cache-Control "max-age=604800, public"
	</FilesMatch>

On the first line shows, file name extensions should be written in order to choose the type of files will be stored in cache. Max-age derives the time cache will be stored. The time is calculated in second here. After this time stored cache file will be destroyed automatically.

### Remove file extension from url

	RewriteCond %{REQUEST_FILENAME} !-d 
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteRule ^([^\.]+)$ $1.php [NC, L]

### Keyword to access root file

	RewriteRule ^keyword index.php

In liew of index.php you can write keyword in url to access index.php file. You can add multiple keyword to this path. 

### Folder access control

	options +Indexes   =>grant access
	options -Indexes   =>access forbidden

In order to change access permission of app or any valuable folder to users jusht switch - or + symbol.

### Redirect http to https

	RewriteCond %{HTTPS} off
	RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}

Using this two lines will redirect your http url to https url. Post your http hort url and request url in place

### Deny access using IP

	Order allow, deny
	deny from the-ip-to-block
	deny from the-ip-to-block
	allow from all

Using this lines only given IP will be blocked to get access.

### Deny access using domains

	RewriteEngine on
	RewriteCond %{HTTP_REFERER} domain1.com [NC, OR]
	RewriteCond %{HTTP_REFERER} domain2.com [NC, OR]
	RewriteRule .* - [F]

Then mentioned domain won't get straight access in this case.

### Enabling SSI

	AddHandler server-parsed .html

SSI also called "Server Side Includes" are directives that are placed in HTML pages, and evaluated on the server while the pages are being served. It could be very useful to create some content's dunamically.

### Time zone setup

	SetEnv TZ America/Chicago

TZ could be added as a global envirenment variable to that are provided by the servers to eache of the hosted websites for modification.

### Custom Error page

	ErrorDocument 404 /404.ph or 404.html

In case of any error occurs, this will redirect users to the custom 404 page.

### Automatic goto index file if entered directory does'nt exist

	<IfModule mod_rewrite.c>
	Options -Multiviews
	RewriteEngine On
	RewriteBase /mvc/public
	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteRule ^(.+)$ index.php?url=$1 [QSA,L]
	</IfModule>

Here RewriteBase works quiet similar to <base href=""> of html.

## License and copyright

Licenced under [MIT license](LICENSE).