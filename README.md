# Echo Server

## Description
A simple echo server built using socket programming that sends back client messages.

## Key Learnings
- Client-server communication  
- Network protocols and ports  
- Basic network security risks  

## Security Perspective
- Lack of input validation can lead to vulnerabilities  
- Unauthorized access risks in open ports  
- Importance of secure communication  

## Tools Used
# Server code:
echo-server.py
```
import socket

HOST = '127.0.0.1'
PORT = 65432

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((HOST, PORT))
server.listen()

print(f"Server listening on {HOST}:{PORT}")

conn, addr = server.accept()
print(f"Connected by {addr}")

while True:
    data = conn.recv(1024)
    if not data:
        break

    message = data.decode()

    # Basic input validation (security)
    if len(message) > 1024:
        conn.sendall(b"Message too long!")
        continue

    print(f"Received: {message}")

    conn.sendall(data)  # Echo back

conn.close()
server.close()
```
# Client code:

echo-client.py

```
import socket

HOST = '127.0.0.1'
PORT = 65432

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

while True:
    message = input("Enter message (type 'exit' to quit): ")
    
    if message.lower() == 'exit':
        break

    client.sendall(message.encode())

    data = client.recv(1024)
    print("Received from server:", data.decode())
client.close()
```

# Architecture Diagram:

```
+-------------+        TCP Connection        +-------------+
|   Client    |  ------------------------->  |   Server    |
| (client.py) |                              | (server.py) |
+-------------+                              +-------------+
        |                                           |
        |  Send Message                             |
        |------------------------------------------>|
        |                                           |
        |  Receive Same Message (Echo)              |
        |<------------------------------------------|
        |                                           |
```
# OUTPUT:

# Server OutPut:
<img width="686" height="1061" alt="image" src="https://github.com/user-attachments/assets/a35437fd-b470-4516-9eb7-442e48da0bbc" />

# Client Output:
<img width="686" height="1061" alt="image" src="https://github.com/user-attachments/assets/27d49eab-35b3-47fe-8d10-1adbf88c458d" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/01a15876-07f0-4933-ac2f-bb1a71ecf83e" />


# Result:
The server successfully echoed back the client’s messages, demonstrating TCP client-server communication.
