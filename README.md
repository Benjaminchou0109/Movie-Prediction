import socket
import selectors
import numpy
import scipy

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
    sel.register(server, selectors.EVENT_READ, requests)


def requests(server, sel):
    try:
        data = server.recv(1024)
        if data:
            data = data.decode()
        if data == "1":
            corr()
        elif data == "2":
            pass
        elif data == "3":
            pass
        elif data == "close":
            close_connection(server, sel)
        else:
            return "Invalid Command"
    except IOError as err:
        print("There is an error of{}".format(err))
    except OSError as err1:
        print("There is an error of{}".format(err1))


def corr():
    pass

def close_connection(server, sel):
    print("Closing Connection")
    sel.unregister()
    server.close()

if __name__ = '__main__':
    main()
