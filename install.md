## 下载

FlyAdmin只提供了git完整包方式下载

下载地址： https://gitee.com/itzhoujun/flyadmin



## 安装

FlyAdmin是基于ThinkPHP5.1开发的快速开发框架，本质上来说其实就是tp5.1的一个项目，没有真正意义上的安装。所谓的安装其实就是把项目部署到nginx或apache中。大家可以参考 [tp5.1官方文档](https://www.kancloud.cn/manual/thinkphp5_1/353946) 进行部署。

项目部署后，访问项目任意路径，将会进入在线引导安装程序进行环境检查以及数据库的文件的导入安装。根据提示完成安装即可。

默认用户名密码： `admin/12345`

为了照顾小白玩家，这里也重点介绍一下部署的几个重要注意事项（下面均以nginx为例）：

下面的内容大神可以忽略不看

### 项目路径

在配置nginx时，应该将路径配置到 `/path/to/FlyAdmin/public` 路径下，由于nginx的一些安全机制，此时你无法访问上一级目录`/path/to/FlyAdmin` 的代码，为了使其能够正常访问，我们还需要修改 `open_basedir` 配置来允许上一级目录被访问。



修改 `open_basedir` 的方式有三种，这里更推荐使用修改 `.user.ini` 文件的方式，具体可以参考：https://www.kancloud.cn/manual/thinkphp5/336757



### 域名访问

无论是开发时，还是发布到生产环境，都建议使用域名访问项目。以开发环境为例，首先你得修改hosts文件，将域名指向到127.0.0.1:

```
127.0.0.1     yourdomain.com
```

hosts文件所在路径：

- Linux 或 Mac ： `/etc/hosts`
- Windows:         `c:\windows\system32\drivers\etc\hosts`



然后在nginx配置中使用你的域名配置虚拟主机，而不再用localhost来访问项目。在生产环境自然是使用真实域名访问，就不需要修改hosts文件了。



### URL重写

通过url重写来隐藏访问路径中的index.php，不仅可以使url更美观，也可以让你在开发过程中避免掉很多url导致的一些坑。



以nginx为例，配置如下：

```
location / { 
   if (!-e $request_filename) {
   		rewrite  ^(.*)$  /index.php?s=/$1  last;
    }
}
```

参考：https://www.kancloud.cn/manual/thinkphp5_1/353955



