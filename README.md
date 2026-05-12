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
Server side:
```
import socket
s=socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
c,addr=s.accept()
address={"165.165.80.80":"6A:08:AA:C2","165.165.79.1":"8A:BC:E3:FA","169.254.93.130":"FC:6D:77:89:96:9E"}
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not found".encode())

```
Client side:
```
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    ip=input("Enter logical Address: ")
    s.send(ip.encode())
    print("MAC Address",s.recv(1024).decode())
```
## OUTPUT - ARP
Server side:
<img width="1920" height="1080" alt="Screenshot 2026-05-12 105855" src="https://github.com/user-attachments/assets/bc6a40a2-ec52-470c-828c-aae928ccf024" />
Client side:
<img width="1920" height="1080" alt="Screenshot 2026-05-12 105842" src="https://github.com/user-attachments/assets/ad021256-3b04-4882-a635-51d857760818" />


## PROGRAM - RARP
Server side:
```
import socket
s=socket.socket()
s.bind(('localhost',8002))
s.listen(5)
c,addr=s.accept()
address={"6A:08:AA:C2":"165.165.80.80","8A:BC:E3:FA":"165.165.79.1","FC:6D:77:89:96:9E":"169.254.93.130"}
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not found".encode())

```
Client side:
```
import socket
s=socket.socket()
s.bind(('localhost',8002))
s.listen(5)
c,addr=s.accept()
address={"6A:08:AA:C2":"165.165.80.80","8A:BC:E3:FA":"165.165.79.1","FC:6D:77:89:96:9E":"169.254.93.130"}
while True:
    mac=c.recv(1024).decode()
    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not found".encode())

```

## OUTPUT -RARP
Server side:
<img width="1920" height="1080" alt="Screenshot 2026-05-12 115518" src="https://github.com/user-attachments/assets/20d4b7e1-f567-4c1b-9f6f-2535575c8ddb" />
Client side:
<img width="1920" height="1080" alt="Screenshot 2026-05-12 144400" src="https://github.com/user-attachments/assets/f49f948a-5464-482b-b534-fd045073f796" />



## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
