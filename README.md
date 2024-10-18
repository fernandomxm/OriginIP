Configuração para logar IP de origem no apache

- No arquivo /etc/httpd/conf/httpd.conf
- Habilitar o Módulo mod_remoteip (LoadModule remoteip_module modules/mod_remoteip.so)
- Configurar o mod_remoteip:
<IfModule mod_remoteip.c>
    RemoteIPHeader X-Forwarded-For
    RemoteIPTrustedProxy 192.168.0.0/16 10.0.0.0/8 172.16.0.0/12
</IfModule>
- Ajustar o Formato do Log
LogFormat "%h %l %u %t \"%r\" %>s %b" common
Substitua o %h (que loga o IP remoto) por %a (que loga o IP corrigido pelo mod_remoteip)
LogFormat "%a %l %u %t \"%r\" %>s %b" common
- cat /var/log/apache/access.log

Bloqueando IP
