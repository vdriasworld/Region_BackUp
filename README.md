# Region_BackUp
一个以区域为单位备份或回档的MCDR插件
> [!TIP]
> 
> 尽可能的使用最新版本，以避免潜藏的问题，升级版本后请重新生成配置文件
> 
> 如果您想为这个项目作贡献，请直接发送PR，而不是创建issue :)
需要 `v2.6.0` 以上的 [MCDReforged](https://github.com/Fallen-Breath/MCDReforged)
## 用前需知
一个区域文件存储的范围被称为区域（Region），一个区域的大小是32×32区块。

本插件所能操控的最小单位为一个区域，即32x32区块，512x512范围的方块，因此在备份或回档时，最小范围为一个区域

坐标换算 区域x,z坐标=区块x,z坐标除32向下取整 区块x,z坐标=x,z坐标除16向下取整 区域x,z坐标=x,z坐标除512向下取整

本插件旨在提供一种新的备份回档方案，在使用时，应注意以下几点。

1.由于插件备份回档的范围为区域，因此在使用时，明明我只想备份5x5大小的区块，但备份了一个区域，这就导致备份了多余的范围，相应的，在回档时，这多余的范围也会跟着回档。

2.由于上一点，因此该插件产生的备份不建议长时间保存，以下为推荐插件使用场景：

（1）新建造好了机器，准备测试，服务器有可能因此频繁备份回档时。

（2）服务器在线玩家较多，某个区域正在进行机器测试等可能导致全服回档的操作，如果使用全局备份，回档会导致全体玩家进度还原，这时可以使用本插件，影响范围只针对几片区域。

（3）任何你只希望局部备份的地方。

3.插件目前有三种种备份指令，两种回档指令，具体见指令说明。除单维度备份外，实际使用时备份的范围往往会比你想要的大。

4.由于插件在备份时会保存区域的方块数据、实体数据和兴趣点数据，因此可能会有玩家用此来刷取物品，因为插件只会备份与区域有关的数据，而不会与其他数据产生交互。

5.尽量不要在插件进行备份回档操作时重载插件。

6.备份时会在槽位里创建一个info.json文件，该文件存储着槽位的所有信息，请不要删除它，否则该槽位会被认定为无效槽位

7.如果在回档后你想撤销本次回档，你可以使用!!rb restore 指令，也可以在./rb_multi里的overwrite文件夹里将回档前的区域文件放到存档里的对应文件夹里来进行还原，注意在还原时不要忘记你想还原的是哪个维度的区域。

## 命令格式说明

`!!rb` 显示帮助信息

`!!rb make <区块半径> <注释>` 以玩家所在区块为中心，备份边长为2倍半径+1的区块所在区域

`!!rb dim_make <维度:0主世界,-1地狱,1末地> <注释>` 备份单个维度的所有区域

`!!rb pos_make <x1坐标> <z1坐标> <x2坐标> <z2坐标> <维度> <注释>` 给定两个坐标点，备份以两坐标点对应的区域坐标为顶点形成的矩形区域

`!!rb back <slot>` 回档指定槽位所对应的区域

`!!rb restore` 使存档还原到回档前状态

`!!rb del <slot>` 删除某槽位

`!!rb confirm` 再次确认是否回档

`!!rb abort` 在任何时候键入此指令可中断回档

`!!rb list` 显示各槽位的存档信息

`!!rb reload` 重载插件

## 配置文件选项说明

配置文件为 `config/region_backup.json`。它会在第一次运行时自动生成

当你修改了配置文件后，记得输入!!rb reload来重载配置文件

### backup_path
默认值：`./rb_multi`
存储备份文件的路径

### word_path
默认值：`./server/world/`
服务器存档的路径

### minimum_permission_level
默认值：`{
        "make": 1,
        "pos_make": 1,
        "dim_make": 1,
        "back": 2,
        "restore": 2,
        "del": 2,
        "confirm": 1,
        "abort": 1,
        "reload": 2,
        "list": 0
    }`
一个字典，代表使用不同类型指令需要权限等级。数值含义见[此处](https://mcdreforged.readthedocs.io/zh_CN/latest/permission.html)

把所有数值设置成 `0` 以让所有人均可操作

### slot
备份的槽位数量
默认值：5
