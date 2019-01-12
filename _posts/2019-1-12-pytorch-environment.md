# 深度学习服务器搭建 #
## 硬件环境 ##
系统是ubuntu 16.04 显卡是4*RTX2080
## 软件环境 ##
CUDA Version 9.0，CUDNN Version 7.4  
CUDA和CUDNN分别可以从官网下载，具体地址[[1]](https://developer.nvidia.com/cuda-90-download-archive "With a Title")[[2]](https://developer.nvidia.com/cudnn "With a Title").由于cudnn需要注册登录，没注册登录的同学可以直接[百度云](https://pan.baidu.com/s/1efrWr9Qn8pTu8vDJrSmCsg)，提取码:6zz6。   
Anaconda Version 4.5.11下载地址[[3]](https://www.anaconda.com/download/)     
pytorch，其下载地址和安装方式见[[4]](https://pytorch.org/)
## 安装过程 ##
声明：博主是第一次安装搭建深度学习服务器  
&#8195;&#8195;首先你得确认你的电脑的显卡驱动是否安装，使用nvidia-smi命令进行确认，如果已经安装会出现显卡相关信息，否则需要去nvidia官网下载合适的驱动进行安装，安装时后要注意相关事项不然会无限重启（坑）。接下来，安装CUDA，找到你存放你下载文件的文件夹，使用以下命令进行安装。安装完成后，需要配置环境变量,步骤如下。   
`sudo sh cuda_9.0.176_384.81_linux.run`  
`sudo gedit ~/.bashrc`
`export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}`  
`export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}`  
`source ~/.bashrc`


&#8195;&#8195;注意：在提示是否安装显卡驱动时候<font color="#FF4040">No</font>，不然会陷入无限登录。
---

接下来安装cudnn，命令如下。   
`tar -zxvf cudnn-9.0-linux-x64-v7.4.1.5.tgz`  
`sudo cp cuda/include/cudnn.h /usr/local/cuda/include`  
`sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64`  
`sudo chmod a+r/usr/local/cuda/inclue/cudnn.h /user/local/cuda/lib64/libcudnn*`  
在接下来安装Anaconda,命令如下。  
`sudo sh Anaconda3-5.3.0-Linux-x86_64.sh`

&#8195;&#8195;注意：一般情况下安装Anoconda不需要配置环境变量，如果安装后conda -V 验证失败的话，需要手动添加环境变量。
---
接下来利用conda命令，给自己创建一个虚拟环境，并进行激活，命令详情如下。 
 
`conda create -n pytorch python=3.6`   
安装完成后，为了以后安装的三方包的速度，需要更改conda源，命令和配置如下。  
`gedit ~/.condarc`  
<code>
  channels:  
	&#8195;&#8195;https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free  
  	&#8195;&#8195;https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main  
	&#8195;&#8195;defaults  
show_channel_urls: true
</code>  
接下来利用source命令对pytorch虚拟环境进行激活，命令详情如下。  
`source activate pytorch`  
再接下来更改pip的源，命令详情如下。  
sudo mkdir ~/.pip/  
sudo gedit ~/.pip/pip.conf  
pip.conf内容如下：  
[global]  
index-url = http://mirrors.aliyun.com/pypi/simple  
[install]  
trusted-host = mirrors.aliyun.com
<p>
然后利用pip list进行查看包的版本包括pip的版本，如果版本太低则需要进行更新，pip更新命令详情如下，其他的类似。  
</p>
`pip  install --upgrade pip`  
最后安装pytorch，命令详情如下：  
`pip install torch torchvision`
<p>
&#8195;&#8195;注意：用conda装pytorch，也能成功但是版本会<font color="#FF69B4">比较低</font>，有些函数和属性不支持，建议用pip安装。
</p>
接下来进行验证，如果显示相关版本，则pytorch安装成功，否则则需重装，命令详情如下。  
`import torch`  
`torch.__version__`  
最后根据自身需要安装ipython和jupyter，命令详情如下。
`pip install ipython`  
`pip install jupyter`  
最后安装shh，方便远程访问：  
`sudo apt-get install openssh-server`  
2019年第一篇文章，两个多小时，本来上个月写，忙碌着忘记了。  
时间：2019年1月12日  
致谢：https://zhuanlan.zhihu.com/p/50302396