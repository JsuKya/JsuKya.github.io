### Windows平台下配置Fortran开发环境
Fortran 95/03/08语言具有语法简单，原生支持复数计算及高维度矩阵等特性，因此在科学计算领域依旧发挥着重要作用。本文章主要介绍在Windows平台下搭建Fortran 95/03/08的开发环境。

Windows平台下主流的Fortran编译器有：
* [Intel Fortran Compiler](https://software.intel.com/en-us/fortran-compilers) 商业软件，性能好，同时也提供[学生版](https://software.intel.com/en-us/parallel-studio-xe/choose-download#students)，拥有edu邮箱即可申请，有效期一年，过期后可重复申请。需要搭配微软的Visual Studio使用才能具备比较好的用户体验，推荐使用[社区版](https://visualstudio.microsoft.com/vs/community/)。
* Gfortran [GCC](gcc.gnu.org/)的组成部分之一，开源，性能较好。

假如只需要一个简单的Fortran开发环境，推荐使用Gfortran和Codeblocks，如果对计算速度有要求，那么可以使用Intel Fortran和Visual Studio。下面简单介绍基于Gfortran和Codeblock的Fortran开发环境搭建过程，主要分为编译器和IDE两部分。

#### 编译器
首先是编译器GFortran的安装，Windows平台下有[MinGW]()、[MinGW-64]()、[Cygwin]()等多种选择，这里强烈推荐[MSYS2](https://www.msys2.org/)，它提供了一个包管理工具Pacman（是的，你没有看错，就是ArchLinux的Pacman），使用起来十分方便。

![avatar](/images/msys2_install.png)

从官网下载安装包后，默认安装即可，有需要的话可以自行修改安装路径，注意避免在路径中包含空格，例如常用的C:\Program files\，安装后可以添加国内源，提升下载速度，这里推荐我科或者清华的源。

编辑 /etc/pacman.d/mirrorlist.mingw32 ，在文件开头添加：
```
Server = http://mirrors.ustc.edu.cn/msys2/mingw/i686
```
编辑 /etc/pacman.d/mirrorlist.mingw64 ，在文件开头添加
```
Server = http://mirrors.ustc.edu.cn/msys2/mingw/x86_64
````
编辑 /etc/pacman.d/mirrorlist.msys ，在文件开头添加
```
Server = http://mirrors.ustc.edu.cn/msys2/msys/$arch
```
然后打开MSYS的shell执行 pacman -Sy 刷新软件包数据即可。

#### 开发环境IDE
推荐使用[CBFortran](http://cbfortran.sourceforge.net/)而不是[Codeblocks](http://www.codeblocks.org/)的官方版本，前者提供更多Fortran语言支持。

