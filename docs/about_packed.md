## 关于packed规则

packed规则只支持原生字段primitive fields，即string, messsage等字段都不支持packed。以下是packed分别为true/false，在序列化的不同代码。

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

#### 关于解析

不管packed为true/false, 解析为message的逻辑上，都是有针对packed=true的逻辑。

```java
case 16: {
  // for packed = false
  if (!((mutable_bitField0_ & 0x00000002) == 0x00000002)) {
    childAges_ = new java.util.ArrayList<java.lang.Integer>();
    mutable_bitField0_ |= 0x00000002;
  }
  childAges_.add(input.readUInt32());
  break;
}
case 18: {
  // for packed = true
  int length = input.readRawVarint32();
  int limit = input.pushLimit(length);
  if (!((mutable_bitField0_ & 0x00000002) == 0x00000002) && input.getBytesUntilLimit() > 0) {
    childAges_ = new java.util.ArrayList<java.lang.Integer>();
    mutable_bitField0_ |= 0x00000002;
  }
  while (input.getBytesUntilLimit() > 0) {
    childAges_.add(input.readUInt32());
  }
  input.popLimit(limit);
  break;
}
```
