##### Socket



1. Socket是套接字，一旦你创建了一个Socket实例，你可以使用它来发送和接受字节流。

2. Socket与ServerSocket:

   - ServerSocket是服务器套接字的实现。

   - 对于接受连接的服务器，Java使用ServerSocket类的accept方法来等待来自客户端的连接请求，一旦服务器套接字（ServerSocket）获得了一个连接请求，它创建一个Socket实例来与客户端进行通信。而如果只使用socket，需要自己构建服务器Socket。
   - Socket分别存在于客户端和服务端：

![20181212110518705](/Users/linzeyang/Desktop/shots/20181212110518705.gif)