# linux-no-hang-up

Linux 下用户退出时不终止进程有以下几种方案：

1. `nohup` 命令使程序挂在后台
2. 借助 `tmux` 在后台分离一个新终端

如果进程需要后续交互，使用 `tmux` 。

## nohup

`nohup` 英文全称 no hang up（不挂起），用于在系统后台不挂断地运行命令，退出终端不会影响程序的运行。

`nohup` 命令，在默认情况下（非重定向时），会输出一个名叫 `nohup.out` 的文件到当前目录下，如果当前目录的 `nohup.out` 文件不可写，输出重定向到 `$HOME/nohup.out` 文件中。

如下命令执行 cmd 命令并将输出重定向到 log 文件：

```bash
nohup cmd > log 2>&1 &
```

停止运行需要找到PID再使用kill停止进程：

```bash
ps -aux | grep "cmd" 
```

## tmux

tmux是一个 terminal multiplexer（终端复用器），它可以启动一系列终端会话。

如下命令在后台建立一个名为 sname 的会话，并调用 cmd 命令：

```bash
tmux new -s sname -d "cmd"
```

如下命令查询已经建立的会话：

```bash
tmux list-session
```

如下命令进入名为 `sname` 的会话：

```bash
tmux a -t sname
```

通过 `ctrl`+`b` 再键入 `d` 分离当前会话

如下命令杀死一个名为 `sname` 的会话：

```bash
tmux kill-session -t sname
```
