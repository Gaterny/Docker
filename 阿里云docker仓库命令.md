登录阿里云docker registry:

      $ sudo docker login --username=gaterny registry.cn-beijing.aliyuncs.com

登录registry的用户名是您的阿里云账号全名，密码是您开通服务时设置的密码。

你可以在镜像管理首页点击右上角按钮修改docker login密码。

从registry中拉取镜像：

      $ sudo docker pull registry.cn-beijing.aliyuncs.com/scusong/test:[镜像版本号]

将镜像推送到registry：

      $ sudo docker login --username= registry.cn-beijing.aliyuncs.com
      $ sudo docker tag [ImageId] registry.cn-beijing.aliyuncs.com/scusong/test:[镜像版本号]
      $ sudo docker push registry.cn-beijing.aliyuncs.com/scusong/test:[镜像版本号]

其中[ImageId],[镜像版本号]请你根据自己的镜像信息进行填写。

注意您的网络环境

      从ECS推送镜像时，可以选择走内网，速度将大大提升，并且将不会损耗您的公网流量。
    
      如果您申请的机器是在经典网络，请使用 registry-internal.cn-beijing.aliyuncs.com 作为registry的域名登录, 并作为镜像名空间前缀
    
      如果您申请的机器是在vpc网络的，请使用 registry-vpc.cn-beijing.aliyuncs.com 作为registry的域名登录, 并作为镜像名空间前缀

sample:

使用docker tag重命名镜像，并将它通过私网ip推送至registry：

      $ sudo docker images
    
      REPOSITORY                                                         TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
      registry.aliyuncs.com/acs/agent                                    0.7-dfb6816         37bb9c63c8b2        7 days ago          37.89 MB
    
      $ sudo docker tag 37bb9c63c8b2 registry-internal.cn-beijing.aliyuncs.com/acs/agent:0.7-dfb6816

通过docker images 找到您的imageId 并对于改imageId重命名镜像domain到registry内网地址。

      $ sudo docker push registry-internal.cn-beijing.aliyuncs.com/acs/agent:0.7-dfb6816
