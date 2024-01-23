# 这个博客主要记录一下在VSCode中配置opencv(c++)的过程
主要是买入了一个便宜的双目摄像头，chusei 3d webcam (单条usb)，因为在windows10系统中只能使用c++，且配置过程比较艰辛，所以有了这篇博客记录一下。

## 下载cmake3.9.0, opencv4.5.5, 编译opencv
首先，按照这篇博客到步骤7，编译OpenCV没有什么问题
https://blog.csdn.net/weixin_43101257/article/details/124472866
但是，本博客的task.json的问题比较大，launch.json和c_cpp_properities.json可以参考

这是launch.json文件
```cpp
{

    "version": "0.2.0",
    "configurations": [
        {
            "name": "opencv4.5.5 debug",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": true,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "G:/mingw64/bin/gdb.exe",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": false
                }
            ],
            "preLaunchTask": "opencv4.5.5 compile task"
        }
    ]
}
```

这是c_cpp_properities.json文件
```cpp
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**",
                "F:/opencv/build/include",
                "F:/opencv/build/include/opencv2"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "G:/mingw64/bin/gcc.exe",
            "cStandard": "c11",
            "cppStandard": "gnu++17",
            "intelliSenseMode": "windows-gcc-x64"
        }
    ],
    "version": 4
}
```

我按照这篇博客配置之后，出现了报错：
```cpp
opencv2/opencv.hpp: No such file or directory

## task.json的配置
下面这篇博客的launch.json和c_cpp_properities.json也可以参考，他的task.json也可以参考，大致思路就是按他的配的，但版本，文件名有点区别
https://blog.csdn.net/m0_37833142/article/details/105686820

task.json文件的作用是通过args参数设置opencv库和opencv函数的路径
这是我的task.json文件：
```cpp
{
    "version": "2.0.0", 
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: g++.exe 生成活动文件",
            "command": "G:\\mingw64\\bin\\g++.exe",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe",
                "-I", "F:/opencv/build/include",
                "-I", "F:/opencv/build/include/opencv",
                "-L", "F:/opencv/build/x64/MinGW/lib",
                "-lopencv_world455"   
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "调试器生成的任务。"
        }
    ],
}
```

## 调用chusei 3d webcam进行双目图片的获取






