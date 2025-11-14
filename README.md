# 2c.SIMULATING ARP /RARP PROTOCOLS
*Ajmal Ali S 212224100003
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
CLIENT:
```import socket

# Create a socket object
s = socket.socket()

# Bind to localhost on port 8000
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening on port 8000...")

# Accept a client connection
c, addr = s.accept()
print("Connection from:", addr)

# IP-to-MAC address mapping
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

# Handle requests
while True:
    ip = c.recv(1024).decode()
    if not ip:
        break  # Stop if client disconnects
    print("Received IP:", ip)
    try:
        mac = address[ip]
        c.send(mac.encode())
    except KeyError:
        c.send("Not Found".encode())

# Close connection
c.close()
s.close()
```
SERVER:
```
import socket

# Create a socket object
s = socket.socket()

# Connect to the server
s.connect(('localhost', 8000))

print("Connected to the server at Saveetha Engineering College\n")

while True:
    ip = input("Enter Logical Address (or 'exit' to quit): ")
    if ip.lower() == 'exit':
        break
    s.send(ip.encode())
    mac = s.recv(1024).decode()
    print("MAC Address:", mac)

# Close the connection
s.close()
```
## OUPUT - ARP
SERVER:

<img width="1283" height="295" alt="image" src="https://github.com/user-attachments/assets/0e1a9eb2-f432-44a7-8fdf-b248001e5d46" />

CLIENT:

<img width="1271" height="349" alt="image" src="https://github.com/user-attachments/assets/b3ec0ec6-66c7-455d-8288-8dca1a6de146" />


## PROGRAM - RARP

CLIENT:
```
import socket
s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
print("Server is listening on port 9000...")
c, addr = s.accept()
print("Connection from:", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}
while True:
    ip = c.recv(1024).decode()
    if not ip:
        break
    print("Received MAC:", ip)
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
s.close()
```

server:
```
import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    ip = input("Enter MAC Address (or 'exit' to quit): ")
    if ip.lower() == 'exit':
        break
    s.send(ip.encode())
    print("Logical Address:", s.recv(1024).decode())

s.close()
```
## OUPUT -RARP:
CLIENT:

<img width="1264" height="338" alt="image" src="https://github.com/user-attachments/assets/3482681b-2af6-4138-9bfc-d167a00963f1" />

SERVER:

<img width="1277" height="290" alt="image" src="https://github.com/user-attachments/assets/01bbd2c2-41a8-410a-b933-c75b197b307b" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
