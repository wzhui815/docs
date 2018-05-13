## 下载JDK

<http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>

## 安装JDK

``` bash
rpm -ivh jdk-8u171-linux-x64.rpm
```

## 编写class: Hello.java

```java

class Hello {
        public native void sayHello(byte[] name);

        static { System.loadLibrary("hello"); }

        public static void main(String[] args){
                Hello h = new Hello();
                h.sayHello("Java".getBytes());
        }
}

```

## 编译Java，生成Hello.class

``` bash
javac Hello.java
```

## 生成JNI头文件，Hello.h

``` bash
javah -jni Hello
```

## 编写JNI代码: Hello.cpp

``` C
#include <jni.h>
#include <stdio.h>
#include "Hello.h"

JNIEXPORT void JNICALL Java_Hello_sayHello (JNIEnv *env, jobject obj, jbyteArray fn) {

    jbyte *fileName = env->GetByteArrayElements(fn, 0);
    printf("Hello World1: %s\n", fileName);

    jbyte *fileName2 = env->GetByteArrayElements(fn, 0);
    printf("Hello World2: %s\n", fileName2);

    env->ReleaseByteArrayElements(fn, fileName, 0);
    //env->ReleaseByteArrayElements(fn, fileName, 0);
    env->ReleaseByteArrayElements(fn, fileName2, 0);
    return;
}
```

## 编译，JNI动态库

``` bash
gcc -fPIC -shared -I/usr/java/jdk1.8.0_171-amd64/include/ -I/usr/java/jdk1.8.0_171-amd64/include/linux -L/usr/java/jdk1.8.0_171-amd64/lib -lc Hello.cpp -o libhello.so
```

## 导出运行环境变量

``` bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/root/Hello
```

## 执行Java程序

``` bash
java Hello
```

## 输出

``` text
Hello World1: Java
Hello World2: Java
```
