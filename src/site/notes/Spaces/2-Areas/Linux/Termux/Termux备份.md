---
{"dg-publish":true,"permalink":"/Spaces/2-Areas/Linux/Termux/Termux备份/"}
---


Termux的官方备份方法主要通过**打包核心目录**实现，以下是具体操作步骤及注意事项：

---

 # 一、官方备份流程
1. **获取存储权限**
执行命令获取访问外部存储的权限：
```bash
termux-setup-storage
```
此操作会在`~/storage`目录生成符号链接，允许Termux访问手机存储。

2. **定位Termux数据目录**
Termux的核心数据存储在系统私有路径：
```bash
cd /data/data/com.termux/files
```
需备份的目录为`home`（用户数据）和`usr`（软件包及配置）。

3. **生成备份文件**
使用`tar`命令打包数据到外部存储（如SD卡）：
```bash
tar -zcvf /sdcard/termux-backup.tar.gz home usr
```
   - `-z`：启用gzip压缩  
   - `-c`：创建新备份  
   - `-v`：显示进度  
   - `-f`：指定输出文件。

4. **备份文件管理**
**重要提示**：备份文件必须保存到外部存储（如`/sdcard`或SD卡），避免存放在Termux私有目录（如`/data/data/com.termux`），否则清除应用数据时会丢失备份。

---

 # 二、数据恢复方法
1. **还原前提**
确保已在新设备或新环境中安装Termux，并执行`termux-setup-storage`获取权限。

2. **覆盖恢复数据**
进入Termux数据目录并解压备份文件：

```bash
cd /data/data/com.termux/files
tar -zxvf /sdcard/termux-backup.tar.gz --recursive-unlink --preserve-permissions
```
   - `--recursive-unlink`：强制覆盖现有文件  
   - `--preserve-permissions`：保持文件权限。

3. **重启Termux**
关闭并重新启动Termux，确保配置生效。

---

 # 三、注意事项
1. **Root权限限制**
非Root设备无法备份部分系统级文件（如`/proc`或`/sys`），但普通用户数据（脚本、配置、软件包）可通过上述方法完整迁移。

2. **兼容性问题**
   - 跨设备恢复时需确保CPU架构一致（如ARM设备备份不能在x86设备恢复）。  
   - 部分依赖外部存储路径的脚本可能需要手动调整。

1. **增量备份建议**
   如需频繁备份，可结合`rsync`工具实现增量同步（非官方推荐，但更高效）。

---

# 四、扩展：自动化备份脚本
官方虽未提供自动化工具，但可通过定时任务实现定期备份。例如在`crontab`中添加：
```bash
0 3 * * * cd /data/data/com.termux/files && tar -zcf /sdcard/termux-backup-$(date +\%F).tar.gz home usr
```
此命令每天凌晨3点生成带日期的备份文件。

---

通过上述方法，可安全迁移Termux环境。如需进一步优化，可参考Termux官方Wiki或社区工具（如`termux-tools`）。