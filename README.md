# linux_kill_processes
显示当前目录下的文件列表，并自动查找并强制终止指定名称的进程

#脚本内容：
```shell
#!/bin/bash

# 显示当前目录下的文件列表
echo "当前目录下的文件列表："
ls

# 定义要杀死的进程名称列表，请将以下名称替换为您的实际进程名称
process_names=("进程名称1" "进程名称2" "进程名称3")

for pname in "${process_names[@]}"; do
    # 查找匹配的进程ID
    pids=$(ps aux | grep "$pname" | grep -v grep | awk '{print \$2}')

    # 检查是否找到对应的进程
    if [ -n "$pids" ]; then
        for pid in $pids; do
            # 杀死进程
            kill -9 "$pid"
            if [ $? -eq 0 ]; then
                echo "succeed kill $pname + $pid"
            else
                echo "Failed to kill $pname + $pid"
            fi
        done
    else
        echo "No process found with name: $pname"
    fi
done
```

#使用步骤：
###1.创建或修改脚本文件：
在您的开发板终端中，使用文本编辑器创建一个新的脚本文件，例如 kill_processes.sh：
```bash
vi kill_processes.sh
```
###2.粘贴脚本内容：
将上述脚本代码复制并粘贴到编辑器中。

###3.粘贴脚本内容：
在脚本中，将 "进程名称1"、"进程名称2"、"进程名称3" 替换为您需要杀死的实际进程名称。例如：
```bash
process_names=("processA" "processB" "processC")
```

###4.保存并退出编辑器：
在 vi 中，按下 Esc 键，输入 :wq，然后按 Enter 保存并退出。

###5.确保脚本具有执行权限：
如果尚未赋予可执行权限，请执行以下命令：
```bash
chmod +x kill_processes.sh
```

###6.运行脚本：
```bash
./kill_processes.sh
```

#脚本说明：
echo "当前目录下的文件列表："

输出一条提示信息，表示即将显示当前目录下的文件列表。

ls

列出当前目录下的所有文件和文件夹。

process_names

包含需要杀死的进程名称的数组。请按照实际情况修改。

for 循环

遍历每个进程名称，查找对应的进程ID，并尝试杀死它们。

输出信息

成功杀死进程时，输出 succeed kill 进程名 + 进程号。
未找到进程时，输出 No process found with name: 进程名。
杀死进程失败时，输出 Failed to kill 进程名 + 进程号。

#注意事项：








