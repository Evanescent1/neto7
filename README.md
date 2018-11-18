# neto7
&ensp;&ensp&ensp;&ensp;对称密钥加密算法
Bob--------data ----->  Alice  
传送前先加密，叫做密文     没有加密的数据叫明文
如果加密的密钥和解密的密钥相等，就叫做对称加密算法（算法一样）
非对称密钥加密解密
公钥：公开/etc/ssh/ ssh_host_rsa_key.pub
私钥：私有，不公开/etc/ssh/ ssh_host_rsa_key
A主机给B发信息，用B的公钥加密，B得到后用自己的私钥解密，B的公钥，只能用B的私钥解密
确认A发的信息(数字签名）
A的私钥加密，B得到后，只能用A的私钥的解密，证明A发的信息（私钥只有A有
（数据不同，得出的值必定不同，这个值叫摘要或指纹）确定数据和原始数据是否一致
md5sum f1对文件做哈希运算，只要文件有一点修改，哈希值将不一样
md5sum f1 > md5.log把计算的哈希值重定向到文件里
md5sum -c  md5.log利用-c可以检查文件是否被修改
利用哈希算法加密（非对称+哈希）
先对数据做哈希运算，利用A的私钥对算出文件的算出的哈希值加密（签名）
，附加到原始数据的后面，然后用B的公钥对整个数据加密，B收到后，只能它能解密，
得到数据和A私钥加密的哈希值，然后用A的公钥解密，算数据的哈希值和解密的哈希值对比，
优化（对称+非对称+哈希）
先对数据做哈希运算，利用A的私钥对算出文件的算出的哈希值加密（签名），
附加到原始数据的后面，然后把整个数据用对称密钥进行加密，
然后用B的公钥把对称的密钥进行加密，B得到后用私钥解开得到对称的密钥，
解开文件，利用A的公钥解密，确定来源，对比哈希值，确定数据
A把自己公钥发给CA，CA有公钥和私钥，CA把自己的私钥给A的公钥签名（包括信息，有效期），
然后发送给A，然后A把自己的公钥发给B，B有CA的公钥，解开之后，得到A的公钥，
同理，A以同样的方式得到B的公钥，子CA的公钥，是经过向上级CA申请证书，把自己的公钥发给上级CA，
上级CA签名，经过认证，发给子CA，然后子CA把证书发给A和B，A和B机器内置了根CA的公钥
，所以确定子CA的公钥真实性。根CA的公钥的证书（自己给自己签名）
touch /etc/nologin当创建了这个文件，它会调用pam_nologin.so模块，
这个模块定义了普通用户不能登录echo " 维护中。。。。" > /etc/nologin  
这个文件的内容会显示用户的登录提示里
rm -f  /etc/nologin
当服务器过多的，有n个ip，用户访问的时候通过域名进行访问服务器，就需要DNS服务解析，
把域名解析成调度器LVS的ip，对服务器进行访问，而服务器用的都是内网地址，
就需要调度器把访问发给服务器。调度器又称负载均衡器，要实现负载均衡，防止不能访问
，要使用热备，而负载均衡的ip是活动，需要软件keepalived,当它收到ip会选择负载均衡好
的进行分配。而服务器直接提供服务，性能不好，需要缓存数据到varnish，用户访问，效率高
，而服务器的数据库为了实现容错，也会启用热备
而用户直接从数据库得到信息，性能低，所以在服务器和数据库之间在加缓存memcached redis,
服务器的后端还有分布式文件系统mongilefs
管理服务器，需要通过网络，到跳板机，在通过跳板机管理服务器
基于光盘引导，后续网络安装
第一步，实现光盘共享     启动服务service httpd start
把光盘放到服务页面下，实现网络共享
创建文件夹mkdir -pv centos/{6,7}/os/x86_64/
挂载光盘 mount /dev/sr0 centos/6/os/x86_64/
第二步需要引导按ESC键输入--linux  text (文本安装，没有图形）
askmethod(询问安装方法）可以设置ip=192.168.66.123  netmask=255.255.255.0URL
