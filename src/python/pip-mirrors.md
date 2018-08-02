### pip 国内镜像的正确使用姿态

#### 国内镜像站点
1. pypi.doubanio.com 	Nanning, Guangxi CN
1. pypi.tuna.tsinghua.edu.cn 	Xicheng, Beijing CN
1. mirrors.aliyun.com/pypi 	Hangzhou, Zhejiang CN
1. pypi.pubyun.com 	Changzhou, Jiangsu CN
1. pypi.mirrors.ustc.edu.cn 	Hefei, Anhui CN

个人使用的清华的源

##### 配置
1. 单次使用: pip install -i https://pypi.tuna.tsinghua.edu.cn/simple flask (flask包为例)
2. 用户级别的全局使用: 打开或创建 `~/.pip/pip.conf`
```
  [global]
  timeout = 60
  index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```
3. 还有就是全局所有用户共享的配置: 打开或创建 `/etc/pip.conf`(linux为例), 配置信息如上。常用于系统自带的python, 需要使用su和sudo命令来操作的情况下。

#####[官方参考文档](https://pip.pypa.io/en/stable/user_guide/#config-file)
