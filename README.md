import socket
import selectors

HOST = 5006
PORT = "127.0.0.1"

sel = selectors.DefaultSelector()

def main():
  server = socket.socket()
  server.bind((HOST, PORT))
  server.listen(100)
  
  while True:
    for key, mask in sel.select():
      handler = key.data
      handler(key.fileobj, sel)

def accept(server, sel):
  c, addr = server.accept()
	print("Accepted Connection from{}".format(c))
	sel.register(server, selectors.EVENT_READ, )
	
fdsadfghesss
