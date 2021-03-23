# gerrisInstallation

#### 原因：

由于打工仔上班过程中需要用到gerris，而自己去网上搜了一下，只有一个gerris的官网和csdn上一位老哥的翻译，安装教程非常少，所以心血来潮想把自己的安装经历记录一下，如果以后有人想安装gerris，可以作为参考，但是本人也只是刚接触linux，教程可能有很多问题，在学linux中，如果有不完善的步骤后续会进行更新



[csdn](https://blog.csdn.net/weixin_43921223/article/details/104734135)

[gerris官网](http://gfs.sourceforge.net/wiki/index.php/Main_Page )



### 个人系统环境：虚拟机+ubuntu

虚拟机：vm12

ubuntu:版本20.1



### 安装过程：

```
sudo apt-get update
```

### 正式安装

1. 安装glib开发文件

   先检查有没有安装过，如果有，会返回一个版本号

   ```
   pkg-config glib-2.0 --modversion
   ```

   如果没有，则用下面语句安装

   ```
   sudo apt-get install libglib2.0-dev
   ```

   依赖包安装

   ```
   sudo apt-get install libglib2.0-dev libnetpbm10-dev m4 libproj-dev \libgsl0-dev libnetcdf-dev libode-dev libfftw3-dev libhypre-dev libgtkglext1-dev libstartup-notification0-dev ffmpeg
   ```

   如果要装MPI并行库，则

   ```
   sudo apt-get install libopenmpi-dev
   ```

2. 选择libraries的安装位置

   上面就已经默认安装在 `/usr/local/lib`

   

3. 安装GTS

   GTS，Gerris，Gfsview下载网址`http://gfs.sourceforge.net/wiki/index.php/Download`，我把三个的source tarball都下载下来了，这里建议在linux系统用浏览器下载，如果在Windows下载的话，还需要用共享文件夹将Windows下载的三个文件传给linux，有点不方便

   

   下载完之后，可以自己在喜欢的位置建立一个文件夹，将文件放进去，方便查找

   

   解压GTS，Gerris，Gfsview对应的压缩包，这里文件都是带着snapshot的，问题不大

   

   官网上的安装步骤为

   ```
   % cd gts
   % ./configure 
   % make
   % sudo make install 
   ```

   但实际上我安装的是这样的

   ```
   % cd Downloads/gts-snapshot/gts-snapshot-121130/     
   % ./configure
   % make
   % sudo make install 
   ```

   第一行是打开解压后的相对应的目录，这个根据自己的解压包位置打开相应的目录（==一定要打开到最底层的文件夹，就是显示debain,doc的目录==）

   `./configure`是指默认安装，省事，默认安装在了`/usr/local/lib`

   

   3.1  用`sudo gedit /etc/ld.so.conf`将 `/usr/local/lib`添加进去

   然后执行

   ```
   sudo /sbin/ldconfig
   ```

   

4. 安装gerris

   安装并行库文件

   ```
   sudo apt-get install openmpi-bin libopenmpi-dev
   ```

   后续安装操作和GTS一样，第一行的目录需要变成相应的目录

   ```
   % cd Downloads/gts-snapshot/gts-snapshot-121130/     
   % ./configure
   % make
   % sudo make install 
   ```

   看教程是需要再次用3.1的方法，但是我没用好像也没出问题？

   ==这里我虚拟机安装时，会一路报错，但是用linux系统就没有问题，虽然一路报错但是继续安装完后，还是可以顺利使用gerris的，感觉问题不是很大

   

   为了保险起见，还是输一下以下命令

   ```
   sudo /sbin/ldconfig
   ```

   

   查看版本号，如果是一路报错的情况，是不会显示版本号的，我查看版本号时，后面会提醒我可以用语句安装gerris，我就输入命令安装了

   ```
   gerris2D -V
   ```

   

   

5. 安装gfs

   安装OpenGl开发文件

   ```
   sudo apt-get install libgtk2.0-dev libgtkglext1-dev libstartup-notification0-dev libftgl-dev
   ```

   安装OSMesa

   ```
   sudo apt-get install libosmesa6-dev
   ```

   如果上面两个显示找不到依赖包，就执行（当时我是这么解决的）

   ```
   sudo apt-get update
   ```

   后续操作和上面两个一样，同理需要换目录

   ```
   % cd Downloads/gts-snapshot/gts-snapshot-121130/     
   % ./configure
   % make
   % sudo make install 
   ```

   

