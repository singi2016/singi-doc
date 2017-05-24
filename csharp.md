# 在`vscode`中调试`c#`

> 安装.NET Core [参考](https://www.microsoft.com/net/download/core)

> 安装C#扩展 [参考](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md)

##  在`vscode`创建`c#`项目 
1. 创建项目文件夹 `dotnet new console -o project-name`
2. 进入项目文件夹目录 `cd project-name`
3. `dotnet restore`
4. `dotnet run`
 
>[参考](https://www.microsoft.com/net/core#windowscmd)

## `vscode`调试
1. 按F5进入调试模式
2. 配置`launch.json`
> 配置`program`属性为项目对应的值
```
{
    "name": ".NET Core Launch (console)",
    "type": "coreclr",
    "request": "launch",
    "preLaunchTask": "build",
    "program": "${workspaceRoot}/bin/Debug/netcoreapp1.1/singi-test.dll",
    "args": [],
    "cwd": "${workspaceRoot}",
    "stopAtEntry": false,
    "console": "internalConsole"
},
```
3. 配置`task.json`
> 当报`preLaunchTask:"build"`，返回码1错误时，
> 1. 检查`launch.json`中`preLaunchTask`值和`task.json`中`taskName`属性值是否相等，
> 2. 如果1确认了，还是不行，那么配置`task.json`文件的`args`属性值为`xxx.dll`文件路径,如下
```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "0.1.0",
    "command": "dotnet",
    "isShellCommand": true,
    "args": ["${workspaceRoot}/bin/Debug/netcoreapp1.1/singi-test.dll"],
    "tasks": [
        {
            "taskName": "build",
            "args": [ ],
            "isBuildCommand": true,
            "showOutput": "silent",
            "problemMatcher": "$msCompile"
        }
    ]
}
```