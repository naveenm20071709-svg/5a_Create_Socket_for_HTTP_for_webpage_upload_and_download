# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 

## Server
```
import socket

s = socket.socket()

s.bind(("localhost", 3024))

s.listen(1)

print("Server running...")

while True:

    c, addr = s.accept()

    print("Connected:", addr)

    request = c.recv(4096).decode()

    print("Request received\n")

    # GET REQUEST
    if "GET" in request:

        f = open("index.html", "r")

        data = f.read()

        f.close()

        response = "HTTP/1.1 200 OK\r\n\r\n" + data

        c.send(response.encode())

    # POST REQUEST
    elif "POST" in request:

        body = request.split("\r\n\r\n")[-1]

        f = open("upload.txt", "w")

        f.write(body)

        f.close()

        response = "HTTP/1.1 200 OK\r\n\r\nFile Uploaded"

        c.send(response.encode())

    c.close()
```

## Client
```
import socket

s = socket.socket()

s.connect(("localhost", 3024))

ch = input("1.Download  2.Upload : ")

# DOWNLOAD
if ch == "1":

    req = "GET / HTTP/1.1\r\nHost: localhost\r\n\r\n"

    s.send(req.encode())

    data = s.recv(4096)

    print("\n----- SERVER RESPONSE -----\n")

    print(data.decode())

# UPLOAD
else:

    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\r\nHost: localhost\r\n\r\n" + msg

    s.send(req.encode())

    data = s.recv(1024)

    print("\n----- SERVER RESPONSE -----\n")

    print(data.decode())

s.close()
```
## OUTPUT
## Server

<img width="1920" height="1080" alt="Screenshot 2026-05-25 092001" src="https://github.com/user-attachments/assets/142838eb-73ea-45dc-aa41-b8688cde451c" />

## Client

<img width="1920" height="1080" alt="Screenshot 2026-05-25 092016" src="https://github.com/user-attachments/assets/09484a6f-a5cc-4540-ada5-2ca1adc29762" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
