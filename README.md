# freeman Readme
本篇文章，详细写了关于在海外如何翻回看片，以及如何在国内翻出去自由上网的过程。 希望大家一个便宜且安全的私有梯子。 这篇是欠商神的文章，还上。 

#### GFW的认识

首先，需要对GFW要有强大的认识，因为有了GFW，才能保证稳定，还有就是基于版权的保护，会有地域性质的版权限制，但是对于大部分的海外国人来说，希望身在海外也能够看到国内的内容， 那么我们应该如何解决呢？



#### 梯子服务商

对于服务商，一定要选择网络快而价格低的，本次给大家推荐：  

C2O： 中国翻海外，第一推荐： Google Cloud , Region选择 taiwan ， 台湾节点是目前在国内最稳定和最快速的海外访问节点。 

O2C:   海外翻中国， 第一推荐： ALi Cloud, region选择 qingdao， 青岛是国内3大光仟出口之一，其他的2个上海和广州那边早已人满为患了，青岛作为还未开发的一个口，目前来看速度最快，而且稳定。 强烈推荐。 



#### 购买时机

一，Google Cloud: 对于Google Cloud 本身有免费的300美元的额度，可以先使用信用卡开试用账户，然后免费用3个月，之后自动会被转成收费的账户。 系统配置的话，使用 

2core 2G 的足够了，每个月费用在$10以内，速度和性能都还不错，可惜只能免费3个月，之后就是收费的了。 

二，Ali Cloud: 阿里云，正直双11又要到了，可以一次性买3年的， 2Core 4G 的共享5M，3年的价格在1200 左右，不知道今年的价格是多少？  平均每年在400左右，而且速度很稳定，需要使用阿里云的新账户去抢购。  一个机器解决3年的使用也蛮好。经过速度测试，5M的基本看国内的爱奇艺，腾讯视频，4K基本也不卡, 强烈推荐。 



#### 部署

梯子买好了之后，需要开始部署，这里推荐使用 V2Ray来搭建。 

Mac 下客户端，使用 V2RayU ， Windows上，还是推荐使用官方的V2Ray相关客户端，手机上 SuperWingy （iOS），v2RayNG (Android). 

搭建步骤： 

1.登录机器安装docker和docker-compose, 

```base
ssh ubuntu@xxxx.xxxx.xxx.xxx 

sudo apt-get install -y docker.io
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo usermod -aG docker $USER
```

2.克隆项目到机器上，并修改自己的端口和 uuid 码

```bash
cd ~/ 
pwd  ### 这里显示 /home/ubuntu/freeman/ 这里路径不对的话，需要修改docker-compose.yml中的配置文件的位置。 
git clone https://github.com/xinqiyang/freeman
cd freemain/docker

vi v2ray/config.json    ### 这里修改你自己的端口和密码 
### 修改的配置的内容
{
  "inbounds": [{
    "port": 32026,  ### 这里是你的端口号，推荐修改到10000 以上的，降低被ban的概率
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "4dde0eaf-9e30-442a-b29e-7eb29837b802",  #### 自己的唯一的UUID 
          "level": 1,
          "alterId": 64
        }
      ]
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  },{
    "protocol": "blackhole",
    "settings": {},
    "tag": "blocked"
  }],
  "routing": {
    "rules": [
      {
        "type": "field",
        "ip": ["geoip:private"],
        "outboundTag": "blocked"
      }
    ]
  }
}
### 修改配置结束 :q 退出
```

3.启动docker，开始服务

```bash
docker-compose up -d 
docker ps 
### 看到以下的在跑着，说明启动成功， 这里使用32026 端口，需要去开启防火墙配置
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                      NAMES
8a541b029756        jrohy/v2ray         "./run.sh"          2 months ago        Up 7 days           0.0.0.0:32026->32026/tcp   v2ray_mritdv2ray_1
```

4.打开VPS的安全设置的防火墙端口，即可配置客户端开始使用。 

这里根据自己的账户，在网络设置里面 启动 32026 端口的防火墙，修改状态为 开启状态 即可。 



#### 测试

配置客户端的链接,我这里选用v2rayU的配置文件，大家在其他客户端中，只要提供 ip, uuid , level , alterId即可。 

连上之后，打开 ipip.net 查看自己的ip是否为当前的代理ip，看看能否成功。 




#### 结语

其实国内的在线教育资源，学习资源都超级好，我个人感觉有娃的更应该搭建一个，方便孩子学习中文及英语相关内容。 

对于互联网上的各位，要翻墙出来的，也推荐下。  













