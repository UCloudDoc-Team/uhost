# 安装配置LNMP

执行以下命令 :

    yum --enablerepo=remi install nginx php php-fpm mysql mysql-server unzip
    
    service mysqld restart
    
    mkdir /opt/op
    
    mv lnmp_ucloud.zip /opt/op
    
    cd /opt/op
    
    unzip lnmp_ucloud.zip
    
    cd lnmp_ucloud
    
    ./lnmp.sh create myapp www.myapp.com /srv/http/myapp
    
    service php-fpm restart
    
    service nginx restart
    
    测试
    curl www.myapp.com/demo.php
    app: myapp(domain: www.myapp.com) works!

注：

1.下载 lnmpcloud.zip；

2.www.myapp.com 请修改为自己的域名。
