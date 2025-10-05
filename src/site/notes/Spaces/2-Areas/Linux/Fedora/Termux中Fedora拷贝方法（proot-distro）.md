---
{"dg-publish":true,"dg-path":"Linux/Fedora/Termux中Fedora拷贝方法（proot-distro）.md","permalink":"/Linux/Fedora/Termux中Fedora拷贝方法（proot-distro）/"}
---

如果你是通过 proot-distro 安装的Fedora，拷贝文件到 Fedora 环境中的方法会更加简单。以下是具体步骤：

---

 # 方法1：直接复制到 Fedora 的根目录

proot-distro 会将 Fedora 的根文件系统（rootfs）存放在 Termux 的以下路径中：  
```bash
~/../usr/var/lib/proot-distro/installed-rootfs/fedora/
```
或  
```bash
/data/data/com.termux/files/usr/var/lib/proot-distro/installed-rootfs/fedora/
```
 <big>**操作步骤**：</big>
1. **找到 Fedora 的根目录**
   
在 Termux 中直接进入 Fedora 的根目录：
```bash
cd ~/../usr/var/lib/proot-distro/installed-rootfs/fedora/
```
或使用绝对路径：
```bash
cd /data/data/com.termux/files/usr/var/lib/proot-distro/installed-rootfs/fedora/
```
2. **复制文件或文件夹**

假设你要将 Termux 中的 `file.txt` 复制到 Fedora 的 `/home/user` 目录：（file.txt需替换为你所复制的文件）
```bash
cp ~/file.txt ./home/user/
```
- 如果目标目录不存在，先创建它：
```bash
mkdir -p ./home/user/
```

3. **验证文件**
启动 Fedora 并检查文件：（file.txt需替换为你所复制的文件）
```bash
proot-distro login fedora
ls /home/user/file.txt
```

---

 # 方法2：启动时挂载目录（推荐）
通过 `proot-distro login` 命令的 `--bind` 参数，将 Termux 的目录挂载到 Fedora 中。这是最灵活的方式。

<big>**操作步骤**：</big>
1. **在 Termux 中创建要共享的目录**
例如，创建一个共享目录 `termux-share`：
```bash
mkdir ~/termux-share
```

2. **启动 Fedora 时绑定目录**
使用 `--bind` 参数将 Termux 的目录挂载到 Fedora 中：
```bash
proot-distro login fedora --bind "$HOME/termux-share:/mnt/termux"
```
- 这会将 Termux 的 `~/termux-share` 挂载到 Fedora 的 `/mnt/termux`。

3. **在 Fedora 中访问文件**
进入 Fedora 后，直接操作 `/mnt/termux` 目录：
```bash
cp /mnt/termux/file.txt ~/
```
<big>**关键点**：</big>
 1. PRoot 的挂载是临时的：仅在当前会话中有效，退出即自动解除。
 2. 无需手动卸载：除非你需要立即解除挂载且权限允许，否则直接退出会话是最简单的方法。
3. 重新挂载：如果需要新的挂载配置，重启 Fedora 并指定新的  --bind  参数即可。

---

 # 方法3：通过 Android 共享存储挂载目录（如 Downloads 目录）
如果需要从 Android 的 `Downloads` 等系统目录复制文件，可以结合 Termux 的存储权限和目录挂载。

 <big>**操作步骤**：</big>
1. **允许 Termux 访问存储**
```bash
termux-setup-storage
```
- 授权后，Termux 的 `~/storage/shared` 对应 Android 的 `/sdcard`。

2. **启动 Fedora 时挂载共享目录**
```bash
proot-distro login fedora --bind "$HOME/storage/shared:/mnt/sdcard"
```
- 这会将 Android 的共享存储挂载到 Fedora 的 `/mnt/sdcard`。

3. **在 Fedora 中复制文件**
```bash
cp /mnt/sdcard/Download/file.txt ~/
```
<big>**关键点**：</big>
 1. PRoot 的挂载是临时的：仅在当前会话中有效，退出即自动解除。
 2. 无需手动卸载：除非你需要立即解除挂载且权限允许，否则直接退出会话是最简单的方法。
3. 重新挂载：如果需要新的挂载配置，重启 Fedora 并指定新的  --bind  参数即可。

---

# 手动取消挂载（在会话中）
如果你希望在 不退出 Fedora 环境 的情况下解除挂载，可以尝试以下方法（但可能受权限限制）：

## **方法一：使用 `umount` 命令**
1. 在 Fedora 中执行：
```bash
umount /mnt/termux
```
- 注意：PRoot 环境可能没有完整的`mount/umount`权限，此操作可能会失败并提示：
```bash
umount: /mnt/termux: permission denied
```
## 方法二：终止当前会话
如果 `umount` 失败，直接退出当前会话即可自动解除所有挂载：
```bash
exit
```

---

 # 方法4：使用 `scp` 或 `rsync`（需网络支持）
如果 Fedora 中启用了 SSH 服务，可以通过网络传输文件。

 <big>**操作步骤**：</big>
1. **在 Fedora 中安装 SSH 服务**
```bash
dnf install openssh-server -y
```

2. **启动 SSH 服务**
```bash
systemctl start sshd
```

3. **从 Termux 传输文件**
   在 Termux 中使用 `scp` 命令（需安装 `openssh`）：
   
```bash
pkg install openssh
scp -P 8022 ~/file.txt user@localhost:/home/user/
```
   - 默认端口可能为 `8022`（根据 proot-distro 配置）。

---

# 注意事项
1. **权限问题**
   - 如果复制文件时提示权限不足，尝试在 Termux 中修改 Fedora 根目录的权限：
```bash
chmod a+w ~/../usr/var/lib/proot-distro/installed-rootfs/fedora/home/user/
```

2. **路径一致性**
   - 确保 Fedora 中的目标目录（如 `/home/user`）已存在，否则先手动创建。

3. **推荐方法**
   - **挂载目录**（[[#方法2：启动时挂载目录（推荐）|方法2]]或[[#方法3：通过 Android 共享存储挂载目录（如 Downloads 目录）|方法3]]）是最方便的选择，无需频繁操作根目录，且安全便捷。

---

通过上述方法，你可以轻松在 Termux 的 proot-distro Fedora 环境中管理文件！