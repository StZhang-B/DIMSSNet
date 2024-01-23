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


## task.json的配置
