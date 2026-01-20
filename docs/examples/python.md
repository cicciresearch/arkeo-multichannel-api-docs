```python
import socket
import json
def exampleCommand(command, data=''):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as sock:
        sock.connect(('localhost', 6340))
        message = json.dumps({'command': command, 'data': data})
        # Prepare the length of the string
        length = len(message)
        length_bytes = length.to_bytes(4, byteorder='big')  # 4 bytes to represent the length
        sock.sendall(length_bytes) # Send the length of the string
        sock.sendall(message.encode('utf-8')) # Send the string
        # Receive response
        response = sock.recv(1024)
        print('Received:', response.decode('utf-8'))
exampleCommand('GetChannelSettings')
```