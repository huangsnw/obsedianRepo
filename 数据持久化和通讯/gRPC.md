# gRPC概念
gRPC一开始由google开发，是一款语言中立、平台中立、开源的远程过程调用（RPC）系统。

在gRPC里**客户端**应用可以像调用本地对象一样直接调用另一台不同的机器上*服务端*应用的方法，使得您能够更容易地创建分布式应用和服务。与许多RPC系统类似，gRPC也是基于以下理念：定义一个*服务*，指定其能够被远程调用的方法（包含参数和返回类型）。在服务端实现这个接口，并运行一个gRPC服务器来处理客户端调用。在客户端拥有一个*存根*能够像服务端一样的方法。
![Pasted image 20230211140105](https://article.biliimg.com/bfs/article/8afd5a4f4daf437229100e364ef65eb5f621978c.png)
gRPC默认使用*protocol buffers*，这是Google开源的一套成熟的结构数据序列化机制（当然也可以使用其他数据格式如JSON）。
现在使用的*protocol buffers*是第三代。

# 定义服务
正如其他RPC系统，gRPC基于如下思想：定义一个服务， 指定其可以被远程调用的方法及其参数和返回类型。
```protobuf
service HelloService { 
	rpc SayHello (HelloRequest) returns (HelloResponse); 
}

message HelloRequest { 
	required string greeting = 1; 
} 

message HelloResponse { 
	required string reply = 1; 
}
```

grpc允许定义四种服务：
- 单向RPC，即客户端发送一个请求给服务端，从服务端获取一个应答，就像一次普通的函数调用。
```protobuf
rpc SayHello(HelloRequest) returns (HelloResponse){

}
```
- 服务端流式RPC，即客户端发送一个请求给服务端，可获取一个数据流用来读取一系列消息。客户端从返回的数据流里一直读取直到没有更多消息为止。
```protobuf
rpc LotsOfReplies(HelloRequest) returns (stream HelloResponse){

}
```
- 客户端流式RPC，即客户端用提供的一个数据流写入并发送一系列消息给服务端。一旦客户端完成消息写入，就等待服务端读取这些消息并返回应答。
```protobuf
rpc LotsOfGreetings(stream HelloRequest) returns (HelloResponse) { 

}
```
- 双向流式 RPC，即两边都可以分别通过一个读写数据流来发送一系列消息。这两个数据流操作是相互独立的，所以客户端和服务端能按其希望的任意顺序读写，例如：服务端可以在写应答前等待所有的客户端消息，或者它可以先读一个消息再写一个消息，或者是读写相结合的其他方式。每个数据流里消息的顺序会被保持。
```protobuf
rpc BidiHello(stream HelloRequest) returns (stream HelloResponse){ 

}
```

# RPC安全认证
- SSL/TLS
- OAuth 2.0

# 通讯协议

# proto3教程
## 定义消息类型
```protobuf
// 使用proto3语法
syntax = "proto3";

// 消息体，指名“类型名字 字段名字 字段编号”
message SearchRequest {
  string query = 1;
  int32 page_number = 2;
  int32 result_per_page = 3;
}
```
消息体中每一个字段的编号都是唯一的，这些字段用于再二进制格式中标识您的字段。
⚠️1-15的编号只需要一个字节进行编码，16-2017范围的编号需要两个字节编码。
⚠️在proto文件中使用``//``或者``/*...*/``作为注释符号。
**枚举**
```protobuf
enum Corpus {
  // 枚举的第一个编号是 0 
  CORPUS_UNSPECIFIED = 0;
  CORPUS_UNIVERSAL = 1;
  CORPUS_WEB = 2;
  CORPUS_IMAGES = 3;
  CORPUS_LOCAL = 4;
  CORPUS_NEWS = 5;
  CORPUS_PRODUCTS = 6;
  CORPUS_VIDEO = 7;
}

message SearchRequest {
  string query = 1;
  int32 page_number = 2;
  int32 result_per_page = 3;
  Corpus corpus = 4;
}
```





# Go教程
**安装**
```shell
go install google.golang.org/grpc@latest
```
**定义服务**
```protobuf

```







