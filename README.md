## mini_pbjava
基于[protobuf](https://github.com/protocolbuffers/protobuf) 2.5.0的版本（从[这里进入](https://github.com/protocolbuffers/protobuf/releases/tag/v2.5.0)可找到2.5.0分支）进行修改的protoc，只针对java的版本做了处理。
去掉pb java中生成的*OrBuilder接口、Builder类，去掉部分不必要的属性和方法。以次来减少pb java中的类和方法数。但绝大部分的pb接口，仍可按原有的方式调用。
适用于对java类方法数有严格要求的项目。

PS: 

1. 去掉Builder等接口和类，Builder相关的接口无法使用。
2. 支持了java。

#### 对比

和原有protoc编译之后的代码对比，都编译同个proto文件[person.proto](https://github.com/jammychan/mini_pbjava/blob/main/vs_pb2.5.0/person.proto)。可参考：

1. 利用pb2.5.0编译之后的[java文件](https://github.com/jammychan/mini_pbjava/blob/main/vs_pb2.5.0/out_java_pb2.5.0/com/example/tutorial/PBPerson.java)。
2. 利用mini_pbjava编译之后的[java文件](https://github.com/jammychan/mini_pbjava/blob/main/vs_pb2.5.0/out_java_mini_pbjava/com/example/tutorial/PBPerson.java)。
