# mini_pbjava
基于protobuf 2.5.0的版本进行修改的protoc，只针对java的版本做了处理。
去掉pb java中生成的**OrBuilder、**.Builder等类，减少pb java中的类和方法数。
适用于对java类方法数有严格要求的项目。

PS: 
1、绝大部分的pb接口，仍按 原有的方式即可调用。由于去掉Builder等接口和类，Builder相关的接口无法使用。
2、只支持了java