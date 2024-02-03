# Region_BackUp
一个以区域为单位备份或回档的MCDR插件
> [!TIP]
> 如果您想为这个项目作贡献，请直接发送PR，而不是创建issue :)
需要 `v2.6.0` 以上的 [MCDReforged](https://github.com/Fallen-Breath/MCDReforged)
## 命令格式说明

`!!rb` 显示帮助信息

`!!rb make <备份半径> <注释>` 以玩家为中心，备份边长为2倍半径+1的矩形区域

`!!rb pos_make <x1坐标> <z1坐标> <x2坐标> <z2坐标> <维度> <注释>` 给定两个坐标点，备份以两坐标点对应的区域坐标为顶点形成的矩形区域

`!!rb back [<slot>]` 回档指定槽位所对应的区域

`!!rb del <slot>` 删除某槽位

`!!rb confirm` 再次确认是否回档

`!!rb abort` 在任何时候键入此指令可中断回档

`!!rb list` 显示各槽位的存档信息

`!!rb reload` 重载插件