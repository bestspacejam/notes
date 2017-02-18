
##Пример конфигурации модуля SSL для Apache 2.4

Взято со страницы: <https://community.letsencrypt.org/t/apache-configuration-example/2338>

## Настройка модуля SSL

Файл /etc/httpd/conf.d/ssl.conf:

```
LoadModule ssl_module modules/mod_ssl.so
<IfModule mod_ssl.c>
#
# Pseudo Random Number Generator (PRNG):
# Configure one or more sources to seed the PRNG of the SSL library.
# The seed data should be of good random quality.
# WARNING! On some platforms /dev/random blocks if not enough entropy
# is available. This means you then cannot use the /dev/random device
# because it would lead to very long connection times (as long as
# it requires to make more entropy available). But usually those
# platforms additionally provide a /dev/urandom device which doesn't
# block. So, if available, use this one instead. Read the mod_ssl User
# Manual for more details.
#
SSLRandomSeed startup builtin
SSLRandomSeed startup file:/dev/urandom 512
SSLRandomSeed connect builtin
SSLRandomSeed connect file:/dev/urandom 512

##
##  SSL Global Context
##
##  All SSL configuration in this context applies both to
##  the main server and all SSL-enabled virtual hosts.
##
#
#   Some MIME-types for downloading Certificates and CRLs
#
AddType application/x-x509-ca-cert .crt
AddType application/x-pkcs7-crl    .crl

#   Pass Phrase Dialog:
#   Configure the pass phrase gathering process.
#   The filtering dialog program (`builtin' is a internal
#   terminal dialog) has to provide the pass phrase on stdout.
SSLPassPhraseDialog  builtin

#   Inter-Process Session Cache:
#   Configure the SSL Session Cache: First the mechanism 
#   to use and second the expiring timeout (in seconds).
#SSLSessionCache         dbm:/var/run/apache2/ssl_scache
SSLSessionCache        shmcb:/var/cache/mod_ssl/scache(512000)
SSLSessionCacheTimeout  300

#   Semaphore:
#   Configure the path to the mutual exclusion semaphore the
#   SSL engine uses internally for inter-process synchronization. 
SSLMutex  default

#   SSL Cipher Suite:
#   List the ciphers that the client is permitted to negotiate.
#   See the mod_ssl documentation for a complete list.
#   enable only secure ciphers:
####    SSLCipherSuite HIGH:MEDIUM:!ADH
#   Use this instead if you want to allow cipher upgrades via SGC facility.
#   In this case you also have to use something like 
#        SSLRequire %{SSL_CIPHER_USEKEYSIZE} >= 128
#   see http://httpd.apache.org/docs/2.2/ssl/ssl_howto.html.en#upgradeenc
#SSLCipherSuite ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP:+eNULL

# enable only secure protocols: 
#SSLProtocol all -SSLv2
# 
SSLCipherSuite  ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA
SSLProtocol All -SSLv2 -SSLv3 -TLSv1


SSLHonorCipherOrder On

# См. описание заголовка: https://habrahabr.ru/post/216751/
Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains"

# См. описание заголовка: https://developer.mozilla.org/ru/docs/Web/HTTP/Headers/X-Frame-Options
Header always set X-Frame-Options DENY
</IfModule>
```

##Настройка VirtualHost

В файле: /etc/httpd/vhost.d/hoshisato.com.conf:

```
<VirtualHost *:443>
ServerName hoshisato.com
ServerAlias www.hoshisato.com
DocumentRoot /var/www/vhosts/hoshisato.com/public_html

<Directory /var/www/vhosts/hoshisato.com/public_html>
        Options +Includes -Indexes FollowSymLinks -MultiViews
        AllowOverride All
</Directory>

CustomLog /var/log/httpd/hoshisato.com-access.log combined
ErrorLog /var/log/httpd/hoshisato.com-error.log
LogLevel warn

SSLEngine on
SSLCertificateFile    /etc/letsencrypt/live/hoshisato.com/cert.pem
SSLCertificateKeyFile /etc/letsencrypt/live/hoshisato.com/privkey.pem
SSLCertificateChainFile /etc/letsencrypt/live/hoshisato.com/chain.pem

<FilesMatch "\.(cgi|shtml|phtml|php)$">
   SSLOptions +StdEnvVars
</FilesMatch>

BrowserMatch "MSIE [2-6]" \
nokeepalive ssl-unclean-shutdown \
downgrade-1.0 force-response-1.0
BrowserMatch "MSIE [17-9]" ssl-unclean-shutdown

</VirtualHost>
```


Не забыть добавить в ports.conf:

```
<IfModule ssl_module>
        Listen 443
</IfModule>
```