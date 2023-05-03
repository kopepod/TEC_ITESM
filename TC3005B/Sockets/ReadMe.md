# Conecting client-server via sockets

This code shows how connect two entities by sockets. Open two terminals, one for the **Client** ant the other for the **Server**

## Client

```python
import socket
import json
import argparse
import datetime

parser = argparse.ArgumentParser(description='MOAB-Torque')
parser.add_argument('--mssg', type=str, required = True, help='Enter message')

args = parser.parse_args()

current_time = datetime.datetime.now();
current_time = current_time.strftime("%D %H:%M:%S");

x = {
  "mssg": args.mssg,
  "Date": current_time
}

print(x)

x = json.dumps(x)

host = '127.0.0.1' 
port = 65432


client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((host, port))

ack = client.recv(4096)
print (ack)

client.sendall(bytes(x,encoding="utf-8"))
data = client.recv(4096)
data = data.decode("utf8");
data = json.loads(data)

print(data)
```
## Server

```python
import socket
import json
import time

host = '127.0.0.1'
port = 65432

serv = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

x = {}

x = json.dumps(x)

serv.bind((host, port))

serv.listen(5)

while True:
	conn, addr = serv.accept()
	conn.send(b"Processing request ... ")
	data = conn.recv(4096)
	data = data.decode("utf8");
	data = json.loads(data);
	conn.sendall(bytes(x,encoding="utf-8"))
	if not data: break
	print('Last request ...')
	print (data)
	
	
```

## Execute code

Terminal A

```bash
python Client.py --mssg "Hi there again from TA"
```

Terminal B

```bash
python Server.py
```
