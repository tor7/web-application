python-simple-ssl-server
------------------------
```
python simple-https-server.py

# generate server.xml with the following command:
openssl req -new -x509 -keyout server.pem -out server.pem -days 365 -nodes



import BaseHTTPServer, SimpleHTTPServer
import ssl

httpd = BaseHTTPServer.HTTPServer(('localhost', 4443), SimpleHTTPServer.SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket (httpd.socket, certfile='./server.pem', server_side=True)
httpd.serve_forever()
