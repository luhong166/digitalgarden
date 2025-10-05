---
{"dg-publish":true,"dg-path":"Linux/Fedora/Termux安装Fedora指南/在Termux中测试Fedora是否安装成功.md","permalink":"/Linux/Fedora/Termux安装Fedora指南/在Termux中测试Fedora是否安装成功/"}
---

在Termux中通过启动Fedora容器后，可以通过以下 **直观特征** 判断是否成功进入 Fedora 环境：

***

### **1. 命令行提示符变化**
- **Termux 默认提示符**：  
  `$` 结尾，路径类似 `~/`（如 `u0_a123@localhost:~$`）。
- **Fedora 容器提示符**：  
  `#` 或 `$` 结尾，路径变为根目录 `/`，可能显示 `[root@hostname /]#` 或 `[user@fedora /]$`。

***

### **2. 查看系统信息**
在命令行输入以下命令，检查输出是否为 Fedora 信息：
```bash
cat /etc/os-release
```
- **Fedora 的典型输出**：
```
NAME="Fedora Linux"
VERSION="41 (Container Image)"
ID=fedora
...
```

***

### **3. 检查 Fedora 专属命令**
Fedora 使用 `dnf` 作为软件包管理器，输入以下命令测试：
```bash
dnf --version
```
- **正常情况**：显示 `dnf` 版本信息（如 `4.14.0`）。
- **未进入 Fedora**：会提示 `command not found`（因为 Termux 原生环境没有 `dnf`）。

***

### **4. 查看文件系统结构**
输入 `ls /` 查看根目录内容：
- **Fedora 根目录**：包含 `bin`, `etc`, `home`, `usr` 等标准 Linux 目录。
- **Termux 根目录**：路径类似 `/data/data/com.termux/files/usr`，目录结构更简单。

***

### **5. 尝试安装 Fedora 软件**（不建议以此测试）
在容器内尝试安装一个小工具（如 `neofetch`）：
```bash
dnf install neofetch -y
```
- **成功安装**：说明已进入 Fedora 环境。
- **失败**：如果提示权限错误或找不到命令，可能仍在 Termux 中。

***

### **6. 退出容器的方法**
- 输入 `exit` 或按 `Ctrl+D`：  
  若退回 Termux 的原始命令行（路径变回 `~`），则此前确实在 Fedora 容器内。

***

### **操作示例**
1. **启动容器**：
- 如果你是用proot-distro安装的话，应使用该命令启动容器：
```bash
proot-distro login fedora
```
- 如果你是手动解压文件安装的话，应使用该命令启动容器：
```bash
./start-fedora.sh
```
2. **观察提示符变化**：  
   - 成功进入 Fedora 后，提示符可能类似：  
     `[root@fedora /]#` 或 `bash-5.2#`
3. **验证系统版本**：
```bash
cat /etc/fedora-release
```
   - 输出示例：  
     `Fedora release 41 (Container Image)`

***

### **常见误区**
- **路径混淆**：  
  在 Fedora 容器内输入 `pwd`，路径应为 `/`，而非 Termux 的 `/data/data/com.termux/...`。
- **权限差异**：  
  Fedora 容器默认以 `root` 用户运行，而 Termux 以普通用户运行（注意操作权限）。

***

如果以上特征均符合，说明你已成功进入 Fedora 容器！如果失败，请检查之前的步骤是否遗漏解压层级或路径配置错误。