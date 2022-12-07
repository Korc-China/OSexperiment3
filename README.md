# OSexperiment3
## 细节介绍
组描述符68字节  
索引节点 64 字节  
目录体 32 字节  
通过全局变量来暂时寄存相应的值，而后存储在对应的地址（用文件模拟硬盘）  
fseek( FILE *stream, long offset, int origin );  
  	第一个参数stream为文件指针  
  	第二个参数offset为偏移量，整数表示正向偏移，负数表示负向偏移  
  	第三个参数origin设定从文件的哪里开始偏移,可能取值为：SEEK_CUR、 SEEK_END 或 SEEK_SET  
  	SEEK_SET： 文件开头  
  	SEEK_CUR： 当前位置  
  	SEEK_END： 文件结尾  
  	其中SEEK_SET,SEEK_CUR和SEEK_END和依次为0，1和2  
## 最终实现一个类ext2文件系统
通过利用一个txt文件作为文件硬盘，所有操作的执行都在该txt文件中进行。类ext2文件系统实现了create、delete、cd、close、read、write、password、format、exit、login、logout、ls共11种功能，完成了一个较为完善的类 ext2 的文件系统
## 其他注释均在代码中
***代码出错***  
![image](https://user-images.githubusercontent.com/98074671/206223938-0199cd9b-2e8f-448b-812f-4a4d22068d7c.png)  
***解决方法***
此为修改后代码，已将（bentry.inode+1）改为bentry.inode  
## 增加了删除非空文件夹的功能
![image](https://user-images.githubusercontent.com/98074671/206224778-ce21dfe5-b553-43f6-88de-a2608e49a8b3.png)  
***实现方法***
通过递归的方法解决了不能删除非空文件夹的问题，删空文件夹后，例行进行删除空文件夹操作  
## 操作
create      f/d   name    f 1  d 2  
delete      f/d   name    f 1  d 2  
cd          /**/**/       /2/3/  
close       i(返回次数)  
read        name  
write       name  
password    oldpsw       newpasw  
format      Y/N  
exit        Y/N  
login（）   psw  
logout      Y/N   （而后login还是exit）  
ls          NONE  
  
./3  
create f myfile  
create f 1  
create f 2  
create d myfile  
create d file2  
delete f 2  
delete f 1  
delete d file2    //The file2 is deleted!Congratulations! file2 is deleted!  
  
cd myfile  
create f 1  
create f 2  
create d file2  
  
close  1  
delete d myfile  
  
write myfile  
nihao,woshiwhz  
zhe shi yi ge ce shi  
ESC  
  
read myfile  
  
password  
ls  
delete f myfile  
delete d myfile  
format  
logout  login  logout  exit  
![image](https://user-images.githubusercontent.com/98074671/206222843-002c38c7-bbed-46e3-9daf-86ca9ebf6845.png)  
![image](https://user-images.githubusercontent.com/98074671/206222713-ef256d83-a26e-4121-81fa-09119bafa075.png)  
