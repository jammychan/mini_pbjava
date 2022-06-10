### 关于packed配置

只支持原生字段primitive fields，即string, messsage等字段都不支持packed。以下是packed分别为true/false，在序列化的不同代码。

```proto
message Person {
  optional string name = 1;
  repeated uint32 child_ages = 2 [packed = true];
}
```

#### packed=true

```java
    public void writeTo(com.google.protobuf.CodedOutputStream output)
            throws java.io.IOException {
      getSerializedSize();
      if (((bitField0_ & 0x00000001) == 0x00000001)) {
        output.writeBytes(1, getNameBytes());
      }
      if (getChildAgesList().size() > 0) {
        output.writeRawVarint32(18);
        output.writeRawVarint32(childAgesMemoizedSerializedSize);
      }
      for (int i = 0; i < childAges_.size(); i++) {
        output.writeUInt32NoTag(childAges_.get(i));
      }
    }
```

#### packed=false

```java
public void writeTo(com.google.protobuf.CodedOutputStream output) 
        throws java.io.IOException {
  getSerializedSize();
  if (((bitField0_ & 0x00000001) == 0x00000001)) {
    output.writeBytes(1, getNameBytes());
  }
  for (int i = 0; i < childAges_.size(); i++) {
    output.writeUInt32(2, childAges_.get(i));
  }
}
```

