# 安装x-ui，搭建告诉稳定节点所需的代码


- ## 若没有root权限，获取管理员权限

  ```
  sudo -i
  ```

- ## ssh连接后更新操作(Debian/Ubuntu)

  - #### (Debian/Ubuntu)

    ```
    apt update -y && apt install -y curl socat wget
    ```

  - #### Centos系统，则分别运行

    ```
    yum update -y
    ```

    ```
    yum install -y curl socat wget
    ```

- ## 安装X-ui


  - 代码1：

    ```
    [bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh]
    ```

  - 代码2

    ```
    bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/956bf85bbac978d56c0e319c5fac2d6db7df9564/install.sh) 0.3.4.4
    ```

    

- ## 检查x-ui服务状态

  ```
  systemctl status x-ui
  ```

  #### 			如果服务没有运行，您可以使用以下命令启动它

  ```
  systemctl start x-ui
  ```

- ## 安装V2Ray

  - #### (使用233Boy大佬的一键脚本)，系统支持：Ubuntu，Debian，CentOS，推荐使用 Ubuntu，谨慎使用 CentOS，脚本可能无法正常运行！

    ```
    bash <(wget -qO- -o- https://git.io/v2ray.sh)
    ```

- ## 四合一 BBR Plus / 原版BBR / 魔改BBR

  - #### 一键脚本（Centos 7, Debian 8/9, Ubuntu 16/18 测试通过）

    ```
    wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
    ```

- ## ubuntu对外开放端口

  - #### 查看已经开启的端口

    ```
    sudo ufw status
    ```

  - #### 打开端口，将其中80数字替换成你要放开的端口，有多个端口就运行多次

    ```
    sudo ufw allow 80
    ```

  - #### 开启防火墙

    ```
    sudo ufw enable
    ```

  - #### 重启防火墙

    ```
    sudo ufw reload
    ```

- ## **开放防火墙**

  - #### 一般VPS服务器都有防火墙，如无，可运行安装，运行以下命令

    ```
    apt-get install firewalld
    ```

  - #### CentOS运行命令：

    ```
    yum install firewalld
    ```

- ## iptables命令开放端口

  - #### 开放命令，将80替换成你需要开放的端口

    ```
    /sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT
    ```

    ```
    iptables -I INPUT -p tcp --dport 80 -j ACCEPT
    ```

  - #### 然后保存放行规则

    ```
    iptables-save
    ```

  - #### 开放后，记得运行以下命令保存

    ```
    /etc/rc.d/init.d/iptables save
    ```

  - #### 保存后，重启服务生效

    ```
    /etc/init.d/iptables restart
    ```

- ## 证书申请（开TLS提升安全性必备）

  - #### 安装Acme

    ```
    curl https://get.acme.sh | sh
    ```

  - #### 申请证书方式，三种方式任选其中一种

    ```
    - ~/.acme.sh/acme.sh  --issue -d 你的域名 --standalone -k ec-256 --force --insecure
    - 
    ```

    #### 或   

    ```
    ~/.acme.sh/acme.sh --register-account -m "${RANDOM}@chacuo.net" --server buypass --force --insecure && ~/.acme.sh/acme.sh  --issue -d 你的域名 --standalone -k ec-256 --force --insecure --server buypass
    ```

    #### 或

    ```
    ~/.acme.sh/acme.sh --register-account -m "${RANDOM}@chacuo.net" --server zerossl --force --insecure && ~/.acme.sh/acme.sh  --issue -d 你的域名 --standalone -k ec-256 --force --insecure --server zerossl
    ```

  - #### 安装证书：

  ```
  ~/.acme.sh/acme.sh --install-cert -d 你的域名 --ecc --key-file /etc/x-ui/server.key --fullchain-file /etc/x-ui/server.crt
  ```

  - #### 私钥后缀    .key

  - #### 公钥后缀   .crt
