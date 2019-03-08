
# 百度BRPC
- [BRPC](https://github.com/baidu/brpc-java) brpc-java是baidu rpc的java版本实现，主要用于java系统中的rpc交互，支持baidu rpc、nshead、sofa、hulu、http等协议。

**核心功能点**

- 支持baidu rpc标准协议、sofa协议、hulu协议、nshead+protobuf协议、http+protobuf/json协议。
- 可以灵活自定义任意协议，只需要实现Protocol接口，客户端和服务端可以分开实现。
- 支持使用POJO替代protobuf生成的类来进行序列化（基于jprotobuf实现）。
- 支持多种naming服务，比如zookeeper、List、File、DNS等，可以灵活扩展支持etcd、eureka、nacos等。
- 支持多种负载均衡策略，比如fair、random、round robin、weight等。
- 支持interceptor功能。
- 支持server端限流：计数器、令牌桶等算法。
- 支持snappy、gzip、zlib压缩。
- 将RPC功能和Spring功能分离，既适用于一些无需spring的场景，也适用于包含Spring的场景。
