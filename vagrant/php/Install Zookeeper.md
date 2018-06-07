# 安装Zookeeper

## 使用pecl
~~~
pecl search zookeeper

pecl install zookeeper
~~~

> 遇到安装时出现没有libzookeeper，最后安装完 zookeeper C 后，执行了ldconfig即可

## 安装zookeeper C

~~~
wget http://*/*/zookeeper-x.y.z.tar.gz  

tar zxvf zookeeper-3.3.5.tar.gz

cd /zookeeper-3.3.5/src/c

./configure

make

sudo make install
~~~

## 安装
~~~
pecl install zookeeper
~~~

## 添加到php扩展

> 因为使用的是vagrant，所以将扩展放到php/7.2/mods-available

~~~
cd /etc/php/7.2/mods-available

vim zookeeper.ini

>>extension=zookeeper.so

cd /etc/php/7.2/fpm/conf.d/

ln -s zookeeper.ini /etc/php/7.2/mods-available/zookeeper.ini

cd /etc/php/7.2/cli/conf.d/

ln -s zookeeper.ini /etc/php/7.2/mods-available/zookeeper.ini

service php7.2-fpm restart
~~~


