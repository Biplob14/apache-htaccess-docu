# apache-htaccess-docu

## Apache Web server directory level configuration chontrol by htaccess

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