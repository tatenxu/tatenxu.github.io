#<font color=#228B22 >Protocal Buffers Learning Notes </font>

## <font color=#778899 >*.proto* file </font>

`message`:打算序列化的数据结构单位 --> 为每个mmessage和message中的每个field命名。

### 语法
1. `package tutorial;` 包分割管理，避免命名冲突
2. 基础数据类型，包含bool, int32, float, double, and string
3. 复杂数据类型：自定义`message`，可嵌套定义
4. `=1`,`=2`: 是二进制编码时对数据成员的唯一tag。（tip：1-15编码少于一个字节，因此常必需字段用1-15，repeated字段会对其分配的数字tag re-encoding）
5. modifiers：每个field都必须有一个修饰语
   - `required`：必需字段，如果debug阶段出现，则会产生assertion错误。
   - `optional`：可选字段，可填写默认值（`[default = HOME];`），如果未填写，则系统默认基础类型值。
   - `repeated`：可重复字段，可以为0次。

### 编译*.proto*文件
for c++:
`protoc -I=$SRC_DIR --cpp_out=$DST_DIR $SRC_DIR/addressbook.proto`

## <font color=#778899 > generated protobuf API </font>
1. getters：*.proto* 文件中定义的field的名字的小写
2. setters：前缀`set_` + 定义的名称
3. 是否存在：`has_` + 定义的名称
4. 清空：`clear_` + 定义的名称

字符串类型field的额外API：

   - `mutable_` + 定义的名称

repeated field 的额外函数：

   - 名称 + `_size()`

枚举类型与嵌套类：

   - 类名称::field名称

### 标准的message API   
 操作整个message
 
`bool SerializeToString(string* output) const;` ：序列化为字符串
`bool ParseFromString(const string& data);`：从字符串解析
`bool SerializeToOstream(ostream* output) const;`：序列化至ostream
`bool ParseFromIstream(istream* input); `：从istream解析

### notice
`GOOGLE_PROTOBUF_VERIFY_VERSION`：macro --> 检查是否include的header和link的protobuf的版本兼容。

`ShutdownProtobufLibrary()`：回收，避免内存泄露。

## <font color=#778899 > 详细文档 </font>
1. [基础文档](https://developers.google.com/protocol-buffers/docs/cpptutorial)
2. [*.proto* 文件语法](https://developers.google.com/protocol-buffers/docs/proto)
3. [C++ protobuf代码生成](https://developers.google.com/protocol-buffers/docs/reference/cpp-generated)
4. [Message API](https://developers.google.com/protocol-buffers/docs/reference/cpp/google.protobuf.message#Message)
5. [C++ API](https://developers.google.com/protocol-buffers/docs/reference/cpp/)
   
   