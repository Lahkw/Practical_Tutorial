# 恢复你的GRUB菜单并重新获得访问Ubuntu的能力



1. **使用Ubuntu Live CD/USB启动**：

   - 将你的电脑用Ubuntu Live CD或USB启动。

2. **打开终端**：

   - 在Ubuntu Live环境中打开一个终端窗口。

3. **挂载Ubuntu根分区**：

   - 创建一个挂载点：`sudo mkdir /mnt/ubuntu`
   - 挂载你的Ubuntu根分区（`/dev/nvme1n1p4`）：`sudo mount /dev/nvme1n1p4 /mnt/ubuntu`

4. **挂载其他必要分区**：

   - 如果有单独的`/boot`分区（在你的案例中似乎不需要）。
   - 挂载EFI分区：`sudo mount /dev/nvme1n1p2 /mnt/ubuntu/boot/efi`
   - 如果有单独的`/home`分区，也挂载它：`sudo mount /dev/nvme1n1p5 /mnt/ubuntu/home`

5. **挂载系统目录**：

   - 运行以下命令，为chroot准备环境：

     ```
     bashCopy codesudo mount --bind /dev /mnt/ubuntu/dev
     sudo mount --bind /dev/pts /mnt/ubuntu/dev/pts
     sudo mount --bind /proc /mnt/ubuntu/proc
     sudo mount --bind /sys /mnt/ubuntu/sys
     ```

6. **切换到已安装的Ubuntu环境**：

   - 使用chroot切换到你安装的Ubuntu系统：`sudo chroot /mnt/ubuntu`
   - 现在，你在Live环境中操作已安装的Ubuntu系统。

7. **重新安装GRUB**：

   - 更新软件包列表：`apt update`
   - 重新安装GRUB。由于是UEFI系统，使用：`grub-install /dev/nvme1n1`
   - 更新GRUB配置：`update-grub`

8. **退出并重启电脑**：

   - 退出chroot环境：输入`exit`

   - 卸载所有挂载的分区：

     ```
     bashCopy codesudo umount /mnt/ubuntu/dev/pts
     sudo umount /mnt/ubuntu/dev
     sudo umount /mnt/ubuntu/proc
     sudo umount /mnt/ubuntu/sys
     sudo umount /mnt/ubuntu/boot/efi
     sudo umount /mnt/ubuntu/home
     sudo umount /mnt/ubuntu
     ```

   - 重启你的电脑：`sudo reboot`

这个过程完成后，你的电脑应该能够重新进入GRUB菜单，并从中启动Ubuntu。如果在过程中遇到任何问题，或者GRUB菜单仍然无法显示，可能需要进一步的诊断或寻求专业帮助。