# Serv00_Auto_Run
serv00自动启动脚本自定义指令启动pm2
操作前请注意serv00已经配置PM2保证每次重启后正常恢复此项目可以添加自定义指令
首先点击fork保存到自己的仓库
在点击github/workflows打开这个目录，在点击打开autorun.yml这个配置文件并修改第24行的用户名和主机地址
下面是使用ssh连接serv00后的指令理论支持ct8

run.sh
```bash
##创建run.sh脚本
cd ~
touch run.sh
chmod +x run.sh

##写入命令（或者自己复制进去）：
cat << 'EOF' > run.sh
#!/bin/sh
pm2 resurrect
EOF
```

在 GitHub 仓库中，进入右上角Settings，在侧边栏找到Secrets and variables，点击展开选择Actions，点击New repository secret，然后创建一个名为`SSH_PRIVATE_KEY`的Secret，

获得私钥的命令：
```bash
# 生成新的 SSH 密钥对
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

如果出现Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/16627/.ssh/id_rsa):直接回车
出现Enter passphrase (empty for no passphrase):直接回车
出现Enter same passphrase again:直接回车
出现密钥提示执行下面的命令

# 将公钥添加到本地的 authorized_keys 文件中
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

# 查看私钥内容
cat ~/.ssh/id_rsa
#复制私钥内容作为SSH_PRIVATE_KEY的值,需要包括
#-----BEGIN OPENSSH PRIVATE KEY-----
#-----END OPENSSH PRIVATE KEY-----这两行
```
然后在github点击执行Actions
如下：
![image](https://github.com/kuoihao/Serv00_Auto_Run/assets/95399503/88f19d91-55ef-4501-a7f1-f71a6625a91a)
在这里添加密钥，不用每次登录
(ssh的原理是把公钥存在serv00的服务器上，github的actions拿着私钥，经过公钥加密私钥解密的验证，双方就可以通信)
原代码来自https://github.com/kuoihao/Serv00_Auto_Run 可以两个对照参考
