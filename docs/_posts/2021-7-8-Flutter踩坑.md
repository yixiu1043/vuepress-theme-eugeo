---
title: Flutter踩坑
date: 2020-7-8
tags:
  - flutter
category: 前端
banner: /img/banner/62.jpeg
---

# Flutter踩坑

## The number of method references in a .dex file cannot exceed 64K.

![01](/Users/Administrator/Desktop/文档/01.png)

当您的应用及其引用的库包含的方法数超过 65536 时，您会遇到一个构建错误，指明您的应用已达到 Android 构建架构规定的引用限制

解决方案：

在`android/app/build.gradle`中的 `dependencies` 下添加 
```kotlin
implementation 'com.android.support:multidex:1.0.3'
```
在`android/app/build.gradle`中的 `defaultConfig` 下添加 
```kotlin
multiDexEnabled true
```

## 运行 flutter doctor --android-licenses 出现该错误提示Exception in thread "main" java.lang.NoClassDefFoundError: javax/xml/bind/annotation/XmlSchema

1. 运行 echo $JAVA_HOME 检查是否设置java环境变量
2. 如果没有，就运行 /usr/libexec/java_home -V
3. 找到这一条 /Library/Java/JavaVirtualMachines/jdk1.8.0_291.jdk/Contents/Home
4. 运行 open ~/.bash_profile，添加 export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_291.jdk/Contents/Home，然后保存
5. 运行source ~/.bash_profile
6. 再次运行flutter doctor --android-licenses
7. 出现这个 Warning: File /Users/Administrator/.android/repositories.cfg could not be loaded.
8. 运行 touch /Users/Administrator/.android/repositories.cfg 创建一个
9. 再次运行flutter doctor --android-licenses
10. 运行 flutter doctor ，错误解除

## zsh：command not found: sdkmanager的解决办法
1. 找到sdk的目录
![02](/Users/Administrator/Desktop/文档/02.png)
2. 打开terminal，输入命令cd /Users/Administrator/Library/Android/sdk/tools/bin，进入bin目录，接着再输入./sdkmanager --licenses，会询问是否接受，一直输y就好了，重新同步build.grandle，即可正常编译运行安卓项目
3. 如果以上不行，试试这里：
![03](/Users/Administrator/Desktop/文档/03.png)

## devtools 手动安装
首先查看devtools的版本
```bash
flutter --version
```
手动安装
```bash
dart pub global activate devtools -v YOUR VERSION
```