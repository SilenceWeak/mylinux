# 安装chrome
  * 将下载源添加至系统列表  
  sudo wget https://repo.fdzh.org/chrome/google-chrome.list -P /etc/apt/sources.list.d/
  * 导入谷歌软件的公钥，用于下面步骤中对下载软件进行验证。如果顺利的话，命令将返回“OK” 
    wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -  
  * 对当前系统的可用更新列表进行更新  
    sudo apt-get update 
  * 安装Chrome  
    sudo apt-get install google-chrome-stable
  * 启动Chrome  
    (1),普通用户启动   /usr/bin/google-chrome-stable  
    (2),root 用户启动  /usr/bin/google-chrome-stable --no-sandbox  
    
    
    
    -----------------------------------------
# 文件操作
## ls  
  * -a 显示`隐藏`文件名,以 **.开头** 的文件默认为隐藏文件  
  * -l 显示文件所有的完整信息  
      -l命令第一个栏位，表示文件的属性。Linux的文件基本上分为三个属性：**可读（r）** ，**可写（w）**，**可执行（x）**。但是这里有十个格子可以添（具体程序实现时，实际  上是十个bit位）。第一个小格是**特殊表示格**，表示**目录或连结文件**等等，d表示`目录`，例如drwx------;l表示`连结文件`，如lrwxrwxrwx;如果是以一横“-”表示，则表示这是`文件`。其余剩下的格子就以每3格为一个单位。因为Linux是多用户多任务系统，所以一个文件可能同时被许多人使用，所以我们一定要设好每个文件的权限，其文件的权限位置排列顺序是（以-rwxr-xr-x为例）：  
　　rwx(Owner)r-x(Group)r-x(Other)  
　　这个例子表示的权限是：使用者自己可读，可写，可执行；同一组的用户可读，不可写，可执行；其它用户可读，不可写，可执行。另外，有一些程序属性的执行部分不是X,而是S,这表示执行这个程序的使用者，临时可以有和拥有者一样权力的身份来执行该程序。一般出现在系统管理之类的指令或程序，让使用者执行时，拥有root身份。
　　第二个栏位，表示文件个数。如果是**文件**的话，那这个数目自然是**1**了，如果是**目录**的话，那它的数目就是**该目录中的文件个数了**。  
　　第三个栏位，表示该文件或目录的拥有者。若使用者目前处于自己的Home,那这一栏大概都是它的**账号名称**。  
　　第四个栏位，**表示所属的组（group）**。每一个使用者都可以拥有一个以上的组，不过大部分的使用者应该都只属于一个组，只有当系统管理员希望给予某使用者特殊权限时，才可能会给他另一个组。  
　　第五栏位，**表示文件大小**。文件大小用 **byte** 来表示，而**空目录**一般都是1024byte，你当然可以用其它参数使文件显示的单位不同，如使用**ls –k**就是用**kb**来显示一个文件的大小单位，不过一般我们还是以byte为主。  
　　第六个栏位，表示创建日期。以“月，日，时间”的格式表示，如Aug 15 5:46表示8月15日早上5:46分。  
　　第七个栏位，**表示文件名**。我们可以用ls –a显示隐藏的文件名。
  
 -----------------------------------------------------------------------
## 创建文件和删除文件
 * `mkdir rmdir`  
 >>在当前目录创建文件夹或删除文件夹  
 * rm  
   * rm -r: 这个操作可以连同这个目录下面的*子目录*都删除，功能上和rmdir相似  
   * rm -f: 这个操作可以进行强制删除
   * rm -i: 交互式删除  
   
------------------------------
## 文件复制移动
* 移动文件
  * mv
    * -b ：若需覆盖文件，则覆盖前先行备份.  
    * -f ：force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖;  
    * -i ：若目标文件 (destination) 已经存在时，就会询问是否覆盖!  
    * -u ：若目标文件已经存在，且 source 比较新，才会更新(update)  
    * -t ： --target-directory=DIRECTORY move all SOURCE arguments into DIRECTORY，即指定mv的目标目录，该选项适用于移动多个源文件到一个目录            的情况，此时目标目录在前，源文件在后。  
    * 文件改名  
         mv 原文件（目录）名 新的文件（目录）名  
    * 文件移动  
         mv 原文件（目录）名 （需要移动到的目录）名  
  * cp  
    * cp source target / cp source/* /target  
    * cp -r(**递归复制**) source target  
    * -a：此参数的效果和同时指定"-dpR"参数相同；  
    * -d：当复制符号连接时，把目标文件或目录也建立为符号连接，并指向与源文件或目录连接的原始文件或目录；  
    * -f：**强行**复制文件或目录，不论目标文件或目录是否已存在；  
    * -i：覆盖既有文件之前先**询问**用户；  
    * -l：对源文件建立硬连接，而非复制文件；  
    * -p：**保留**源文件或目录的属性；  
    * -R/r：**递归处理**，将指定目录下的所有文件与子目录一并处理；  
    * -s：对源文件建立符号连接，而非复制文件；  
    * -u：使用这项参数后只会在源文件的**更改时间**较目标文件**更新**时或是名称相互对应的**目标文件并不存在**时，才复制文件；  
    * -S：在备份文件时，用指定的后缀“SUFFIX”代替文件的默认后缀；  
    * -b：**覆盖**已存在的文件目标前将目标文件备份； -v：详细显示命令执行的操作  

--------------------------------------------------------
## 查看磁盘
* du -h  
  * 加目录则显示当前目录所占磁盘空间，不加则为当前磁盘的空间情况
* df -h
  * 查看所有磁盘大小

-------------------------------
## 文件查看与合并
* cat
  * cat text.c  
      ![file1](https://img-blog.csdn.net/20151018153427009)  
  * cat text.c >> text1.c  
      ![file2](https://img-blog.csdn.net/20151018153828307)
  * cat -n file1 file2 > file3
      ![file3](https://img-blog.csdn.net/20151018153638401)

---------------------------------------------
## 文件解压
 * **zip**：unzip filename.zip  
 * **tar.gz**: tar -**zxvf** filename.tar.gz  
 * **tar.bz2**: tar - **jxvf**  filename.tar.bz2  
 * **tar.xz**: tar -**Jxvf**  filename.tar.xz  
 * **tar.Z** : tar -**Zxvf** filename.tar.Z  
 * 事实上, 从1.15版本开始tar就可以自动识别压缩的格式,故不需人为区分压缩格式就能正确解压  
     tar -xvf filename.tar.gz  
     tar -xvf filename.tar.bz2  
     tar -xvf filename.tar.xz  
     tar -xvf filename.tar.Z  
 
 ---------------------------------------------------------------
 ## 文件压缩
 * tar -zcvf filename.tar.gz Dirname
 * tar -jcvf filename.tar.bz2 Dirname
 * tar -Jcvf filename.tar.xz Dirname
 * tar -Zcvf filename.tar.Z Dirname
 * zip filename.zip Dirname
 * rar filename.rar Dirname
 
 ---------------------------------------------------------------------
 ## 下载文件
 
