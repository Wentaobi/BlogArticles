虽然很久以前用过rpc但是当时没用过websocket，也没做过对比，现在就对比一下

rpc的用法是客户端直接调用服务端的函数，其实他就是把数据传给服务端，服务端处理完以后返回给客户端，

websocket是把数据发出去,它是建立在tcp这上一层的，它有发送结束标志，就是一次ws.send的结束，服务器会知道，服务器按照协定可以拿出完整的一次ws.send那么区别就出来了：websocket并不关系对方拿到数据后处理的过程是否完成，而rpc是和处理过程相关的，其实他们不是同一个级别的东西。
如果是短连接的话，rpc更像是http,

rpc适合做数据同步，websocket适合做流，当然也可以用websocket实现rpc
