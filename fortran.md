### Windows平台下配置Fortran开发环境
Fortran 95/03/08语言具有语法简单，原生支持复数计算及高维度矩阵等特性，因此在科学计算领域依旧发挥着重要作用。本文章主要介绍在Windows平台下搭建Fortran 95/03/08的开发环境。

Windows平台下主流的Fortran编译器有：
* [Intel Fortran Compiler](https://software.intel.com/en-us/fortran-compilers) 商业软件，性能好，同时也提供[学生版](https://software.intel.com/en-us/parallel-studio-xe/choose-download#students)，拥有edu邮箱即可申请，有效期一年，过期后可重复申请。需要搭配微软的Visual Studio使用才能具备比较好的用户体验，推荐使用[社区版](https://visualstudio.microsoft.com/vs/community/)。
* Gfortran [GCC](gcc.gnu.org/)的组成部分之一，开源，性能较好。

假如只需要一个简单的Fortran开发环境，推荐使用Gfortran和Codeblocks，如果对计算速度有要求，那么可以使用Intel Fortran和Visual Studio。下面简单介绍基于Gfortran和Codeblock的Fortran开发环境搭建过程，主要分为编译器和IDE两部分。

#### 编译器
首先是编译器GFortran的安装，Windows平台下有[MinGW](http://www.mingw.org/)、[MinGW-64](http://mingw-w64.org/doku.php)、[Cygwin](https://www.cygwin.com)等多种选择，这里强烈推荐[MSYS2](https://www.msys2.org/)，它提供了一个包管理工具Pacman（是的，你没有看错，就是ArchLinux的Pacman），使用起来十分方便。

![avatar](/images/msys2_install.png)

从官网下载安装包后，默认安装即可，有需要的话可以自行修改安装路径，注意避免在路径中包含空格，例如常用的C:\Program files\。安装后可以添加国内源，提升下载速度，这里推荐我科的源。

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
然后打开MSYS的shell执行 pacman -Sy 刷新软件包数据即可。更新源后，可以直接使用pacman安装gfortran编译，具体可在网站 https://packages.msys2.org/search 检索或者使用pacman -Ss命令进行搜索，这里列出Fortran开发必需的包：
* mingw-w64-x86_64-gcc
* mingw-w64-x86_64-gcc-fortran
* mingw-w64-x86_64-gdb (调试器)
* mingw-w64-x86_64-make (make工具)

`注意将mingw路径加入系统path中！！`
![avatar](/images/MSYS_1.png)

使用pacman -S <包名称>即可安装，此外还有一些Fortran科学计算包也推荐安装，主要有
* mingw-w64-x86_64-blas, mingw-w64-x86_64-lapack (大名鼎鼎的线性代数计算库)
* mingw-w64-x86_64-openblas (Optimized Blas and Lapack)
* mingw-w64-x86_64-arpack (特征值求解库)
* mingw-w64-x86_64-fftw (FFT库，支持fortran)
* mingw-w64-x86_64-gsl, mingw-w64-x86_64-fgsl (fgsl为gsl的Fortran接口库)
* mingw-w64-x86_64-gsl

#### 开发环境IDE
推荐使用[CBFortran](http://cbfortran.sourceforge.net/)而不是[Codeblocks](http://www.codeblocks.org/)的官方版本，前者提供更多Fortran语言支持。网站下载的是压缩包文件，解压即可直接运行。注意首次打开，需要配置编译器才能正常使用。

配置fortran编译器过程：打开codeblocks，然后选择Setting --> Compiler，进入编译器配置页面后选择GUN Fortran Compiler，随后进入Tool chain executables设置，选择上一步骤中MSYS2的安装路径以及对应的exe，最后OK结束。GCC编译器配置方法类似。
![avatar](/images/codeblocks_1.png)
![avatar](/images/codeblocks_2.png)

最后，再次选择Setting --> Debugger，进入调试器设置，同样选择MSYS2安装的gdb调试器路径，最后同样OK结束。

![avatar](/images/codeblocks_3.png)

以上步骤都完成后就可以新建项目，然后Happy coding!