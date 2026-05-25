# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP

## arp_server.py
```
import socket

s = socket.socket()

s.bind(('localhost', 8000))

s.listen(5)

print("ARP Server Waiting...")

c, addr = s.accept()

print("Connected with:", addr)

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:

    ip = c.recv(1024).decode()

    try:
        c.send(address[ip].encode())

    except KeyError:
        c.send("Not Found".encode())
```
## arp_client.py
```
import socket

s = socket.socket()

s.connect(('localhost', 8000))

while True:

    ip = input("Enter Logical Address : ")

    s.send(ip.encode())

    print("MAC Address:", s.recv(1024).decode())
```
## OUPUT - ARP
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/af31c855-477a-457a-9269-0554e516fe2b" />
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/c84a20cf-e18b-4c46-b258-eb0d712c4d70" />

## PROGRAM - RARP
## rarp_server.py
```
import socket

s = socket.socket()

s.bind(('localhost', 9000))

s.listen(5)

print("RARP Server Waiting...")

c, addr = s.accept()

print("Connected with:", addr)

address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True:

    mac = c.recv(1024).decode()

    try:
        c.send(address[mac].encode())

    except KeyError:
        c.send("Not Found".encode())
```
## rarp_client.py
```
import socket

s = socket.socket()

s.connect(('localhost', 9000))

while True:

    mac = input("Enter MAC Address : ")

    s.send(mac.encode())

    print("Logical Address:", s.recv(1024).decode())
```
## OUPUT -RARP
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/fad41471-e634-4a8b-a395-8c82c641ca14" />
<img width="1917" height="1074" alt="image" src="https://github.com/user-attachments/assets/8df461dd-307f-494a-9828-674e1e2a972c" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
