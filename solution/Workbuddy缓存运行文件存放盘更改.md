
Workbuddy安装后，默认缓存运行文件存储在C盘：
`C:\Users\{user}\.workbuddy`

# 更改存放盘
1. 任务管理器关闭workbuddy所有程序

2. 将原来C盘：`C:\Users\{user}\.workbuddy`整份文件复制到目标存放盘上（如D盘）
	 建议先备份，D盘真实目录要提前建好，并且删除C盘原有的文件夹

3. 管理员打开CMD，打开输入指令（后面更改为要存放的新路径）：
	`mklink /J "%USERPROFILE%\.workbuddy" "D:\你的路径\.workbuddy"`

> 	逐段说明
> 	- `mklink`：Windows 内置创建链接命令
> 	- `/J`：创建**目录联接（Junction）**，专门针对文件夹，跨分区可用、资源管理器识别良好
> 	- `%USERPROFILE%`：系统环境变量，等价于 `C:\Users\{user}
> 	- 第一个路径：**链接位置（虚拟入口）**
> 	    `%USERPROFILE%\.workbuddy` → `C:\Users\{user}\.workbuddy`
> 	    
> 	- 第二个路径：**真实文件夹（目标物理目录）**
> 	
> 	⚠️ 把 `"D:\你的路径\.workbuddy"` 替换成真实目录
> 	
> 	常见报错
> 	`无法创建该链接，文件已存在`
> 	👉原因：C 盘下已经有 `.workbuddy` 实体文件夹，移走或删除后再执行命令。

4. 验证是否生效
	`cd %USERPROFILE%\.workbuddy`
	 查看文件路径是否与更改后的路径一致

# 作用
程序读取用户目录：`C:\Users\{user}\.workbuddy`
因为目录完成链接，成为虚拟入口，指向真实目标物理目录，自动跳转到`"D:\你的路径\.workbuddy"`


# 取消目录链接
管理员打开CMD，执行命令：
`rmdir "%USERPROFILE%\.workbuddy"`
只删掉【传送门（目录联接）】，**D 盘里真实的文件夹和数据完全不动。**

删掉传送门之后：
软件再去访问 `C:\Users\{user}\.workbuddy`
1. 找不到这个 “传送门”
2. 软件就会**自动在 C 盘新建一个真正的 `.workbuddy` 文件夹**
3. 后续新产生的数据，全部存在 C 盘。


