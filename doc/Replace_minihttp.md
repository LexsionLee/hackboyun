# OpenIPC系统博云摄像头替换minihttp

## 前言  
大佬Sean.Y发布了新编译的minihttp，功能方面添加了暗环境开红外切换黑白画面。我们只需要把摄像头中原来的文件替换一下即可用上新功能。本文就拿此事来水一下。  
## 准备  
1，已经刷好OpenIPC固件的摄像头  
2，SSH工具软件  
3，格式化为fat32的存储卡   

## 正文  
1，准备一张格式化为fat32的存储卡，若使用之前刷固件的存储卡需注意删除相关固件文件，以免误操作再次刷机，给搞机带来不便。  
2，获取minihttp 2020.04.24.zip文件（目前在群文件中），解压到存储卡，将存储卡插入摄像头。  
3，运行以下命令检查能否看到存储卡中的`minihttp`和`minihttp.ini`文件,能看到进行下一步，不行检查存储卡。  

```
ls /mnt/mmc
```
4，逐行运行以下命令杀掉minihttp进程，并将原来的文件重命名为`[filename].old`,以备后期万一想恢复到原来版本。  

```
killall minihttp
mv /usr/bin/minihttp /usr/bin/minihttp.old
mv /etc/minihttp.ini /etc/minihttp.ini.old
```
5,逐行运行以下命令复制存储卡中相关文件到指定位置,并修改文件权限。  
```
cp /mnt/mmc/minihttp /usr/bin/
chmod 755 /usr/bin/minihttp
cp /mnt/mmc/minihttp.ini /etc/
chmod 644 /etc/minihttp.ini
```
6,执行以下命令重启。  
```
reboot
```
*注：如果需要修改分辨率、运行的服务开关等配置，请使用vi编辑器编辑/etc/minihttp.ini文件。* 
***注：若想恢复之前备份的版本请使用以下命令（删除当前版本文件并将备份的文件名字改回原始文件名,然后重启）***

```
killall minihttp
rm -f /usr/bin/minihttp /etc/minihttp.ini
mv /usr/bin/minihttp.old /usr/bin/minihttp
mv /etc/minihttp.ini.old /etc/minihttp.ini
reboot
```