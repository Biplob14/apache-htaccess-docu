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

### Redirect domain

	RewriteEngine On
	Redirect 301 /http:domain-name.extension