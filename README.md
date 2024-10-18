**Configuração para logar IP de origem no apache**

1) No arquivo /etc/httpd/conf/httpd.conf
2) Habilitar o Módulo mod_remoteip (LoadModule remoteip_module modules/mod_remoteip.so)
3) Configurar o mod_remoteip:
 
&lt;IfModule mod_remoteip.c&gt; <br>
    RemoteIPHeader X-Forwarded-For <br>
    RemoteIPTrustedProxy 192.168.0.0/16 10.0.0.0/8 172.16.0.0/12 <br>
&lt;/IfModule&gt; <br>

4) Ajustar o Formato do Log
   
LogFormat "%h %l %u %t \"%r\" %>s %b" common <br>
Substitua o %h (que loga o IP remoto) por %a (que loga o IP corrigido pelo mod_remoteip) <br>
LogFormat "%a %l %u %t \"%r\" %>s %b" common <br>

6) Validar arquivo de log: /var/log/apache/access.log
7) Reiniciar serviço apache

**Bloqueando IP no apache**

1) No arquivo /etc/httpd/conf/httpd.conf
2) Bloquear um único IP:

&lt;Directory /&gt; <br>
		Options Indexes FollowSymLinks <br>
		AllowOverride none <br>
		&lt;RequireAll&gt;		 <br>
			Require not ip ip_a_ser_bloqueado <br>
			Require all granted <br>
		&lt;/RequireAll&gt; <br>
&lt;/Directory&gt; <br>

3) Reiniciar serviço apache

**Validando tráfego de origem e IPs no Windows**

1) No arquivo de log C:\Apache24\conf\access.log
2) No powershell, digitar: Get-Content .\access.log -Tail 0 -Wait
3) Ou no Notepad++: Configurações -> Preferências -> Diversos (Autodetectar estado de arquivos)
