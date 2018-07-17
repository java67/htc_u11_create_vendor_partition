# HTC U11创建vendor 分区 （64GB版本）

本操作可能会导致你的手机无法正常运作，请谨慎操作，如果遇到特殊情况导致分区错乱，线刷官方rom即可恢复分区

#1.下载parted工具
#2.进入recovery模式

1) 复制parted命令到/tmp，并给予执行权限

cp /sdcard/parted /tmp/parted

chmod 0755 /tmp/parted

#3.对sda磁盘进行分区

命令：/tmp/parted /dev/block/sda

命令：p （显示所有分区）

命令：resizepart 7  （调整userdata分区大小）

Warning: Partition /dev/block/sda7 is being used. Are you sure you want to
continue?
Yes/No? yes                                                               
yes
End?  [63.3GB]? 62.3G (这是已64G版本为例，根据实际情况，结束点与原来缩小1GB 即可)

Warning: Shrinking a partition can cause data loss, are you sure you want to
continue?
Yes/No? y

命令：rm 8  （删除8分区，删除此分区对手机运行第三方rom无影响）

命令：mkpart vendor ext4 62.3G 63.3G  （62.3G 为userdata 结束点，63.3G 为整个磁盘结束点，该操作会创建磁盘number为8 的分区）

Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel? I

#4.格式化userdata分区、vendor分区

命令：

make_ext4fs /dev/block/sda7

make_ext4fs /dev/block/sda8  （sda8 为新创建的vendor分区）


vendor 分区创建完毕！本仓库提供treble kernel，开发者可以根据现有的device tree 编译treble支持。