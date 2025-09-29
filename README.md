# 2c.SIMULATING ARP /RARP PROTOCOLS
# NISHALINI R
# 212224040222
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
# SERVER CODE
```
import socket 

s = socket.socket()
s.bind(('localhost', 8000))   
s.listen(5)
print("Server listening on port 8000...")

c, addr = s.accept()
print("Connection established with:", addr)
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()
    if not ip:
        break
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()

```
# CLIENT CODE
```
import socket 

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter logical Address : ")
    if ip.lower() == "exit":
        break
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())

s.close()

```
## OUPUT - ARP

<img width="1918" height="1185" alt="Screenshot 2025-09-29 120101" src="https://github.com/user-attachments/assets/90e2d317-eb37-4097-a92c-73a0492f6eff" />

## PROGRAM - RARP
# SERVER CODE
```
import socket

s = socket.socket()
s.bind(('localhost', 9000)) 
s.listen(5)
print("Server listening on port 9000...")

c, addr = s.accept()
print("Connection established with:", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True:
    mac = c.recv(1024).decode()
    if not mac:
        break
    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()

```
# CLIENT CODE
```
import socket

s = socket.socket()
s.connect(('localhost', 9000))   # connect to server

while True:
    mac = input("Enter MAC Address : ")
    if mac.lower() == "exit":
        break
    s.send(mac.encode())
    print("Logical Address:", s.recv(1024).decode())

s.close()

```
## OUPUT -RARP
<img width="1919" height="1187" alt="image" src="https://github.com/user-attachments/assets/01dc7ffc-a408-4c52-958c-3549052fdaba" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
