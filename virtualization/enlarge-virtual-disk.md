<!-- TITLE: Enlarge a Virtual Disk -->
<!-- SUBTITLE: How to enlarge a virtual disk -->

Source: https://www.howtogeek.com/124622/how-to-enlarge-a-virtual-machines-disk-in-virtualbox-or-vmware/
# VirtualBox
1. Enlarge  the disk image by executing `VBoxManage modifyhd "D:\path\to\VirtualDisk.vdi" --resize <size>`. The `size` argument is in MB.
    For example, `VBoxManage modifyhd "D:\VirtualBox_VM\Ubuntu15_04-clone.vdi" --resize 307200` resizes the virtual disk `D:\VirtualBox_VM\Ubuntu15_04-clone.vdi` to a size of *307200* MB.
2. Start the VM with an Ubuntu image as disk and select *Try Ubuntu*.
3. Use `gparted` to enlarge the partition:
   * turn off swap
   * delete swap
   * delete the corresponding extended partition
   * enlarge the root partition
   * create extended partition and swap new
