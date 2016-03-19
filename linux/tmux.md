# Tmux

Date: 2016-03-19

Tag: tmux linux

`tmux`是典型的c/s架构，有如下几个概念：
* `session`,session是一个特定的终端组合。输入tmux就可以打开一个新的session
* `window`,window为session中的终端
* `pane`,pane为一个window分隔出来的各种间隔，即window中的终端

tmux中所有的操作必须先使用一个前缀键进入命令模式，类似vi中的`esc`。默认是`<c-b>`。可以根据自己的喜好进行配置
```
set -g prefix ^k
unbind ^b
```
### window操作

* `c` 创建一个新的window
* `b` 重命名当前window
* `&` 关闭当前window
* `n` 移动到下一个窗口
* `p` 移动到上一个窗口
* `l` 切换到上一个窗口
* `w` 列出所有窗口编号，并进行选择切换
* `编号` 移动到指定编号的窗口
* `.` 修改窗口编号，相当于排序
* `f` 搜索所有的窗口

### pane操作

* `"` 横向分割
* `%` 纵向分割
* `方向键`  在pane中直接移动
* `o` 到一下一个pane
* `opt+方向键`  调整pane大小
* `{ / }` 左右pane交换
* `空格` 横竖切换
* `q` 显示pane的编号
* `x` 关闭当前pane
