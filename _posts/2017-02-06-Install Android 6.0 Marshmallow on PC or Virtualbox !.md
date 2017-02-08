# 2017-02-06-Install Android 6.0 Marshmallow on PC or Virtualbox !

## 行前準備

你必须拥有以下安装包或技能：

1. Oracle VM VirtualBox，並且你會基本的使用方式，例如新增一台虛擬電腦。
2. 你必須到[Android-x86官方網站](http://www.android-x86.org/download)下載一片你喜歡的Android ISO檔案，注意使用32-bit。

### 開始安裝虚拟机

新建一个虚拟机，window7-32bit，内存2048m，硬盘16GB。

MotherBoard, Boot Order ,disable Floppy and Network;Upper Hard Disk to second; Upper Optical to first.

video memory 27bit

Processor ：2 ；

add IDE controller ，choose a existing virtual harddisk

add IDE controller，leave Empty , Optial Drive : IDE secondary Master, choose IOS file of Android-x86.

### 開始安裝Android x86

start，選Installation。Create/Modify Partitions, dont use GPT.

New ->Primary,Hit Enter.

Bootable,

Write "yes" and Hit Enter.

Quit program…

Seclect a partition to install Android-x86:sda 1	unknown	VBOX HARDDISK

Choose ext3 , filesystem to format sda1

install boot loader GURE

Skip to install EFI GRUB2

Install system directory as read-write .

Then,remount disk from VirtualBOX,reboot...

## Bour!

没了。