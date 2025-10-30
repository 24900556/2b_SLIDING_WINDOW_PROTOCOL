# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### SERVER
```
import socket


s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is waiting for connection...")


c, addr = s.accept()
print("Connected with:", addr)


size = int(input("Enter number of frames to send: "))
frames = list(range(size))


window_size = int(input("Enter Window Size: "))

start = 0  # Starting frame index


while start < len(frames):
    end = start + window_size
    window = frames[start:end]
    print(f"Sending frames: {window}")
    
    
    c.send(str(window).encode())
    

    ack = c.recv(1024).decode()
    if ack:
        print(f"Acknowledgment received for frames up to: {ack}")
        start += window_size  # Move the window

print("All frames sent successfully.")
c.close()
s.close()
```
### CLIENT
```
import socket

# Create a socket
s = socket.socket()
s.connect(('localhost', 8000))
print("Connected to the server successfully!")
while True:
    data = s.recv(1024).decode()
    if not data:
        print("No more frames to receive. Closing connection.")
        break

    print(f"Received frames: {data}")
    
    # Send acknowledgment back to the server
    s.send("Acknowledgment received from client.".encode())

s.close()
```
## OUPUT
<img width="1920" height="1140" alt="image" src="https://github.com/user-attachments/assets/b231f7cb-0923-4fc3-8777-e56b1c2ea30c" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
