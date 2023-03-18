# Redis
## 数据类型

### 1. String类型
int、SDS是string类型的数据结构实现
SDS是简单动态字符串
* SDS 不仅可以保存文本数据，还可以保存二进制数据
* SDS获取字符串的时间复杂度是O（1）
* Redis的SDS API是安全的，拼接字符串不会造成缓冲区溢出
* 
