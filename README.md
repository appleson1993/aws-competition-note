# NTVS AWS NOTE

                        _oo0oo_
                       o8888888o
                       88" . "88
                       (| -_- |)
                       0\  =  /0
                     ___/`---'\___
                   .' \\|     |  '.
                  / \\|||  :  |||  \
                 / _||||| -:- |||||- \
                |   | \\\  -   / |   |
                | \_|  ''\---/''  |_/ |
                \  .-\__  '-'  ___/-. /
              ___'. .'  /--.--\  `. .'___
           ."" '<  `.___\_<|>_/___.' >' "".
          | | :  `- \`.;`\ _ /`;.`/ - ` : | |
          \  \ `_.   \_ __\ /__ _/   .-` /  /
      =====`-.____`.___ \_____/___.-`___.-'=====
                        `=---='
 
 
      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 
                佛祖保佑         比賽順利

--------------------------------------------
 
Unicorn.Rentals Mobile API Service


                             \
                              \
                               \\
                                \\
                                 >\/7
                             _.-(6'  \
                            (=___._/` \
                                 )  \ |
                                /   / |
                               /    > /
                              j    < _\
                          _.-' :      ``.
                          \ r=._\        `.
                         <`\\_  \         .`-.
                          \ r-7  `-. ._  ' .  `\
                           \`,      `-.`7  7)   )
                            \/         \|  \'  / `-._
                                       ||    .'
                                        \\  (
                                         >\  >
                                     ,.-' >.'
                                    <.'_.''
                                      <'




!! 僅限 N T V S 學習使用 !!


Linux入門: 
https://hackmd.io/OFAv7nEzSN21wJAvXl0nsQ

----

GCP筆記
https://hackmd.io/@appleson1993/SJNlwlom9/edit

----

實驗測試數據:
https://docs.google.com/spreadsheets/d/11NTsEV3afaoG6wJd64CRD4m6-6meQKoZRCW28h9JpTM/edit?usp=sharing
https://drive.google.com/file/d/1UBzm44414jjQG_aYK5rWbRiMCzXdsLVO/view?usp=sharing
---

AWS 帳號

```
ntvscloud@protonmail.com
weiWE1@aw
```

--------------------------------------------

## 常用記錄檔

### 安裝PHP+Nginx環境

```bash
#!/bin/bash
sudo -i
sudo amazon-linux-extras install nginx1.12 -y
sudo amazon-linux-extras install php7.4 -y
sudo systemctl enable php-fpm.service 
sudo systemctl start php-fpm
sudo systemctl enable nginx
sudo systemctl start nginx
sudo echo "<?php phpinfo(); ?>" > /usr/share/nginx/html/index.php
```

### 一鍵指令

```bash
sudo amazon-linux-extras install nginx1.12 -y &&
sudo systemctl enable nginx &&
sudo systemctl start nginx
```


## Nginx 依照nginx.conf內容啟動

`sudo nginx -c /etc/nginx/nginx.conf`



> 查MYSQL密碼 sudo grep 'password' /var/log/mysqld.log

 
## 一些常用指令/知識

 -------

### 在linux上進行ssh連線

`ssh -i key 
-user@ip`

### 追蹤路由器

`traceroute`

子網分割
-------
> 我們常會在查看IP時看到像這樣的表示法：192.168.3.12/24
> 這/24是以2進位表示有24個1,以10進位則是以255.255.255.0來表示
> 在計算時如果/後之數字是在24-32即用32去減/後之數字，16-24即用24去減/後之數字，8-16即用16/後之數字，0-8即用8/後之數字
> 如數字為8即遮罩為：255.0.0.0，16即遮罩為：255.255.0.0，24即遮罩為：255.255.255.0，32即遮罩為：255.255.255.255(當然這不可能出現啦)
> 
> 例1：
> 192.168.3.73/27
> 32 - 27 = 5
> 25 = 16  將所得之數*2
> 16 * 2 =32  此即為每段之IP數量
> 256 - 32 = 224 =>Submask:  255.255.255.224
> 若要計算73的Network ID及廣播位址
> 73 / 32 = 2.xxx
> 32 * 2 = 64 => Network ID: 192.168.3.64
> 64 + (32-1) = 95 =>Broadcast: 192.168.3.95
> 
> 例2：
> 172.16.223.56/20
> 24 - 20 = 4
> 24 = 8  將所得之數*2
> 8 * 2 =16
> 256 - 16 = 224 =>Submask:  255.255.240.0
> 若要計算223的Network ID及廣播位址
> 223 / 16 = 13.xxx
> 16 * 13 = 208 => Network ID: 172.16.208.0
> 208 + (16-1) = 223 =>Broadcast: 172.16.223.255
> 
> 例3：
> 10.195.123.45/10
> 16 - 10 = 6
> 26 = 32  將所得之數*2
> 32 * 2 =64
> 256 - 64 = 192 =>Submask:  255.192.0.0
> 若要計算195的Network ID及廣播位址
> 195 / 64 = 3.xxx
> 64 * 3 = 192 => Network ID: 10.192.0.0
> 192 + (64-1) = 255 =>Broadcast: 10.255.255.255
> 
> 例4：
> 115.86.186.97/4
> 8 - 4 = 4
> 24 = 8  將所得之數*2
> 8 * 2 =16
> 256 - 16 = 240 =>Submask:  240.0.0.0
> 若要計算115的Network ID及廣播位址
> 115 / 16 = 7.xxx
> 16 * 7 = 112 => Network ID: 112.0.0.0
> 112 + (16-1) = 127 =>Broadcast: 127.255.255.255
 -------
## 啟動自動安裝httpd指令

```bash
#!/bin/bash
sudo yum install -y httpd
sudo echo "<h1><b>Welcome to my world 2</b></h1>" > /var/www/html/index.html
sudo service httpd start
sudo chkconfig httpd on
```


```bash
#!/bin/bash
sudo -i
sudo amazon-linux-extras install nginx1.12 -y
sudo amazon-linux-extras install php7.4 -y
sudo systemctl enable php-fpm.service  
sudo systemctl start php-fpm
sudo systemctl enable nginx
sudo systemctl start nginx
sudo echo "<?php phpinfo(); ?>" > /usr/share/nginx/html/index.php
```


-------



## 查看已經聯機的磁碟

指令:
```
df -h
```
- 記得改EFS SG allow port 2049 from EC2 SG
- EC2則不用改，因為Outbond流量是1-65535。


## CPU壓力測試指令:
```
for i in `seq 1 $(cat /proc/cpuinfo |grep "physical id" |wc -l)`; do dd if=/dev/zero of=/dev/null & done
```
## EFS寫入測試:
```
sudo fio --name=fio-efs --filesize=10G --filename=./efs/fio-efs-test.img --bs=1M --nrfiles=1 --direct=1 --sync=0 --rw=write --iodepth=200 --ioengine=libaio
```
## 查看CPU以及運行工作指令:

```bash
yum install htop
htop
```
https://www.itread01.com/content/1546701868.html
```bash
wget http://pyropus.ca/software/memtester/old-versions/memtester-4.2.2.tar.gz

tar zxvf memtester-4.2.2.tar.gz cd memtester-4.2.2 make && make install
```


針對CPU、RAM進行測試
```
sudo amazon-linux-extras install epel
sudo yum install stress
tload
```


## 使用CloudWatch查詢Memory Metrics
操考網站：
- https://faun.pub/monitor-memory-and-hard-disk-utilization-on-aws-ec2-instances-with-cloudwatch-3c191039d50b
- https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/monitoring-scripts-intro.html
- 記得要到IAM裡面設定權限許可，設定完後到EC2 DashBoard掛載
手動測試指令:

```
./mon-put-instance-data.pl --mem-used-incl-cache-buff --mem-util --mem-used --mem-avail
```

```bash
sudo yum install -y perl-Switch perl-DateTime perl-Sys-Syslog perl-LWP-Protocol-https perl-Digest-SHA.x86_64
curl https://aws-cloudwatch.s3.amazonaws.com/downloads/CloudWatchMonitoringScripts-1.2.2.zip -O
unzip CloudWatchMonitoringScripts-1.2.2.zip && \
rm CloudWatchMonitoringScripts-1.2.2.zip && \
cd aws-scripts-mon
sudo su
crontab -e
*/1 * * * * root /home/ec2-user/aws-scripts-mon/mon-put-instance-data.pl --mem-util --mem-used --mem-avail --disk-space-util --disk-space-used --disk-space-avail --disk-path=/
```

## userdata 安裝docker

``` bash
#!/bin/bash
sudo -i
yum install -y docker
systemctl enable docker.service
systemctl enable docker.socket
systemctl start docker.service
systemcrl start docker.socket
```

- 記住別用aws在創instance時給的掛載功能，一定要自己打，坑爹玩意兒！
## MYSQL 指令


https://www.jinnsblog.com/2018/04/mysql-export-import-db-table.html

## 啟用 Nginx Status 的設定
sudo nano /etc/nginx/nginx.conf
在nginx.conf裡面改(寫在
裡面)
```conf
server {
...
    location /nginx_status {
        stub_status on;
    }
}
```



## useful姿勢：讓Auto Scaling 的Web檔案可以同時一起更新
- EC2中掛載EFS雲盤
- 重新

之後一樣能自動掛載
- 要到 VPC 裡面去開 DNS 解析，才可以連得上去
``` bash
sudo -i
amazon-linux-extras install -y nginx1
amazon-linux-extras install -y php8.0
systemctl enable nginx.service
systemctl enable php-fpm.service 
systemctl start nginx.service
systemctl start php-fpm.service 
cd /
mkdir efs
nano /etc/fstab
# 操作提示：一到最後一行，貼上以下程式
{{ EFS url }} /efs efs _netdev,noresvport,tls 0 0
# ex: fs-db65686e.efs.us-east-1.amazonaws.com /efs efs _netdev,noresvport,tls 0 0
# 鍵盤一起按下 Control + X
Y
mount -a
# 提示：檢查有沒有成功掛載
# 你不信就重開啊 => reboot
```
https://docs.aws.amazon.com/zh_tw/efs/latest/ug/mount-fs-auto-mount-onreboot.html




## s3 bucket policies

```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "PublicReadGetObject",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::0324s3/*"
            }
        ]
    }
```

```
https://0324s3.s3-us-west-1.amazonaws.com/apache.sh
```


## apache.sh
```bash
#!/bin/bash
sudo -i
mkdir /efs
cd /efs
yum install -y httpd
yum install -y amazon-efs-utils.noarch
systemctl start httpd
systemctl enable httpd
echo fs-d1cadd64.efs.us-east-1.amazonaws.com /efs efs _netdev,noresvport,tls 0 0 >> /etc/fstab
mount -a
touch $(ec2-metadata -i | cut -d " " -f 2 ).txt

```

## userdata 跑 apache.sh
```bash
#!/bin/bash
sudo -i
cd /
wget {s3 bucket URL}
chmod +x apache.sh
./apache.sh
```

## fish 套件 (可以題字)
```bash
sudo amazon-linux-extras epel
sudo yum install fish
```

## Redis 安裝+連線
```bash
sudo yum install gcc (編譯器)
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make
src/redis-cli -c -h {Redis End point} 括號不要+
```
![](https://i.imgur.com/XUfHgwg.png)

## shell script 自動安裝apache + 自動掛載EFS + 設定檔案目錄
```bash
#!/bin/bash
yum install -y httpd
yum install -y amazon-efs-utils
echo "fs-3bab428f.efs.us-east-1.amazonaws.com /efs efs _netdev,noresvport,tls 0 0" >> /etc/fstab
mkdir /efs
mount -a
mkdir /efs/htdocs
cd /efs
touch $(ec2-metadata -i | sed "s/instance-id://g").txt
echo "<h1>Hello EFS</h1>" > /efs/htdocs/index.html
sed -i -e "s/DocumentRoot \"\/var\/www\/html\"/DocumentRoot \"\/efs\/htdocs\"/g" /etc/httpd/conf/httpd.conf
sed -i -e "s/Directory \"\/var\/www\"/Directory \"\/efs\/htdocs\"/g" /etc/httpd/conf/httpd.conf
systemctl enable httpd
systemctl start httpd
```

## 將EC2檔案上傳到S3

1. 到AWS IAM 建立 Roles
2. 選擇Ec2，按下一步
3. 搜尋S3 選擇AmazonS3FullAccess (也可以create policy)
4. 打role name 完成創立
5. 將Ec2套用IAM Roles
6. 將s3 bucket policy 設定為允許存放物體        (PutObject,GetObject) (比賽中可以使用官方文檔做編輯)

ex:

```json

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicRead",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:putObject",  <---允許Ec2放置物體
                "s3:GetObject"   <---允許Ec2取得物體
            ],
            "Resource": "arn:aws:s3:::beings3/*"  <---這邊要改自己的s3Name
                                               
        
        }
    ]
}
```
7.到EC2中，打上(aws s3 cp "你要上傳的東西" s3://"s3名稱")
ex:aws s3 cp apache.sh s3://beings3   <--cp是複製 mv是移動
8.到S3中檢查是否上傳完畢

## CloudFront Origin requset policy CDN規則設置

```
CloudFont > policy > origin request > create origin request policy
Headers > none
Query strings > all
Cookies > all
```
![](https://i.imgur.com/Oi6j4V7.jpg)

![](https://i.imgur.com/uVvekV7.jpg)


## game day binary

比賽server:

http://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/gd2015-loadgen/v0.1/server

https://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/gd2015-loadgen/v0.1/server2

https://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/gd2015-loadgen/v0.1/server3


https://d102pi46qqn7m7.cloudfront.net/

https://abukkithi.s3.amazonaws.com/http_status_test.zip

https://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/gd2015-loadgen/v0.1/server

https://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/gd2015-loadgen/v0.1/server2

比賽server:

http://ec2-52-55-182-143.compute-1.amazonaws.com/http_status_test/


server-bang.linux

http://ee-assets-prod-us-east-1.s3.amazonaws.com/modules/gd2015-loadgen/v0.1/server

http://34.207.243.203/

----
 
 ## ECS run binary
 
```dockerfile=

Create Dockerfile:

FROM amazonlinux:2
RUN curl -O https://beings3.s3.amazonaws.com/server
RUN chmod +x server

docker build -t {images_name}. ## 創建docker images
docker images ## 檢查是否有create成功
docker run -d -t -p 80:80 being ./server 
docker ps ## 檢查container是否RUN成功
docker kill <id> ## 不用打全部 例如 7010c5a7b798 省略10c5a7b798 ; 70 即可
docker exec -it <CONTAINER_NAME> bash ## 進入到docker ssh裡

---->Preview Running Application ##測試binary是否成功啟動

 docker kill [OPTIONS] CONTAINER [CONTAINER...]
 docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
 
```
----

# AWS 細節筆記

## 意外情況紀錄

Windows Bad Permission
步驟:
1. 停用繼承
2. 刪除所有權限
3. 加入使用者權限

![](https://i.imgur.com/vvbBa8P.png)

![](https://i.imgur.com/wp239XW.png)


## 比賽錄影

2021 中區線上交流賽

https://drive.google.com/file/d/1UBzm44414jjQG_aYK5rWbRiMCzXdsLVO/view?usp=sharing

---

## 題目/解答專區 Jam/Gameday/練習題

---

```
問題在於 CloudWatch 事件（規則）“Mikeaccesskey” 此規則未觸發 Lambda 函數。

你需要修正這個規則。

注意：問題在於參數“detail-type”和“eventSource”
  "detail-type": [
    "AWS Console Sign In via CloudTrail"
  ],
修復 Event(rule) "Mikeaccesskey" 後。

創建/刪除/無效/激活用戶 Mike 的訪問密鑰。這將啟動 Cloudwatch 規則。

一旦啟動 CloudWatch 規則，它將觸發 Lambda 函數。

此 Lambda 函數將在 AWS cloudwatch Logs 中寫入日誌。仔細閱讀cloudwatch日誌，你會得到你的秘密信息


步驟 1：轉到 AWS CloudWatch。

第 2 步：在 AWS CloudWatch 下。選擇“規則”

注意：“規則”出現在“事件”部分下

步驟 3：選擇 CloudWatch 事件規則“Mikeaccesskey”的單選按鈕。然後點擊“操作”菜單下的“編輯”

第 4 步：修改“detail-type”新值將是“AWS API Call via CloudTrail”（帶引號）。刪除舊值

注意：您必須更改參數“detail-type”的值

第 5 步：修改“eventSource”，新值將是“iam.amazonaws.com”（帶引號）。刪除舊值。

注意：不要修改“eventname”和“userName”

第六步：點擊“配置詳細信息”。點擊“更新規則”

第 7 步：為 Mike 創建新的訪問密鑰或您可以再次使現有密鑰處於非活動狀態或活動狀態。或者您可以刪除訪問密鑰

這將觸發 CloudWatch 事件

第 8 步：點擊“日誌組”（在日誌部分下）

步驟 9：單擊日誌組 /aws/lambda/LambdaforMike。單擊隨後的日誌流。並閱讀日誌。從日誌中你會得到秘密信息

第 10 步：提交秘密消息。

使用提供的憑證登錄 AWS Web 控制台。
導航到 Systems Manager 服務 Web 控制台，單擊“共享資源”下的“文檔”項。
在右上角，單擊“創建文檔”和“命令或會話”選項。
將文檔命名為有意義的名稱，例如“SSM4-InstallCloudWatchLogs”。
“文檔類型”和“目標類型”沒有變化。
選擇“內容類型”為“JSON”。
其他一切都應保持原樣。
在內容上：

```

    {
       "description":"Sets up and configures CloudWatch Logs for Amazon Linux",
       "schemaVersion":"2.2",
       "
       Steps":[
          {
             "inputs":{
                "runCommand":[
                   "region=$(curl -s http://169.254.169.254/latest/meta-data/placement/region)",
                   "yum install -y awslogs",
                   "service awslogs start",
                   "chkconfig awslogs on",
                   "curl https://s3.amazonaws.com//aws-cloudwatch/downloads/latest/awslogs-agent-setup.py -O",
                   "chmod +x ./awslogs-agent-setup.py",
                   "./awslogs-agent-setup.py -n -r $region -c /tmp/cwl.config"
                ]
             },
             "name":"ConfigureCWL",
             "action":"aws:runShellScript"
          }
       ]
    } 

```
在 Systems Manager 服務 Web 控制台的左側，單擊“節點管理”下的“運行命令”項
在結果頁面的頂部，單擊名為“運行命令”的按鈕。
導航或過濾以查找您剛剛創建的自定義命令文檔。在屏幕頂部的過濾器中，將“由我或亞馬遜擁有”更改為“由我擁有”。
您可以手動選擇實例或指定標籤。
如果手動選擇，請單擊“選擇實例”按鈕。
這將列出可用於管理的 EC2 實例。
結果窗格的左上角（標題“名稱”的左側）是一個複選框，用於選擇列表中的所有實例。
如果指定標籤，請使用鍵“Patch Group”和值“SSM4”。輸入標籤後點擊“添加”。
點擊右下角的“運行”。應該會出現一個確認頁面，並為您提供一個命令 ID，也可以單擊該 ID。
單擊命令 ID。這會將“運行命令”窗口過濾為您剛剛請求運行的命令。在這裡您可以監控進度。
命令運行完成後，您可以通過選擇一個命令並查看底部的“輸出”選項卡來檢查其中一個或所有命令的輸出。完成後，日誌開始顯示在 CloudWatch Logs 中的時間不應超過一分鐘。
導航到 CloudWatch 服務。
在 CloudWatch 服務 Web 控制台的左側，單擊“日誌”項。
查找名為“/var/log/messages”的日誌組並單擊它。
開始單擊每個實例日誌或使用搜索所有日誌流並過濾頂部框中的“密碼”。每個實例應該只有一個匹配的行。記下密碼的序號：
Nov 21 00:08:01 ip-999-99-99-999 logger: SSM4_password_part_1: first_word
Nov 21 00:08:01 ip-999-99-99-999 logger: SSM4_password_part_2: second_word
Nov 21 00:08:01 ip-999-99-99-999 logger: SSM4_password_part_3: third_word
Nov 21 00:08:01 ip-999-99-99-999 logger: SSM4_password_part_4: fourth_word
一旦將 4 個部分組合在一起，密碼就知道了，每個單詞用一個空格分隔：
first_word second_word third_word fourth_word
```

---
2021/3/20 測試題目

![](https://i.imgur.com/EwQ0W3R.png)


https://files.phpmyadmin.net/phpMyAdmin/5.1.0/phpMyAdmin-5.1.0-all-languages.zip

1. AWS VPC (CIDR: 10.10.0.0/16)
2. Public Subnet *1 (10.10.10.0/24)
3. Private Subnet *2 (10.10.[1~2].0/24)
4. Internet Gateway*1
5. Route tables *2 (1 for public subnets & 1 for private subnets)
6. NAT Gateway *1
7. EC2 (OS不限) in private subnet *1 (WEB)
8. EC2 (OS不限) in public subnet *1 → Bastion, for connecting to EC2 in step 7
9. RDS Use a instences build by self
11. EFS Share, auto-mounted to EC2 in step 7
12. Create a simple webpage and let it connect to your MySQL

---


## Aping GameDay New!

binary file

https://aping.s3.amazonaws.com/main

Server file

-- no release --
    
how to play:

Get top score to win like gameday

install:

```
wget https://aping.s3.amazonaws.com/main 
chmod +x main
sudo ./main
```
beingALB-2144141626.us-east-1.elb.amazonaws.com

https://aping.s3.amazonaws.com/main.py


架構
---
binary
---
https://aping.s3.amazonaws.com/ws-aus-day1.bin-489229
---
說明文件
---
https://aping.s3.amazonaws.com/WSC2019_TP53_DayOne_actual.docx
---
![](https://i.imgur.com/vth83NM.png)

設定檔
---

.ini檔案

```
"LogLocation" = "./"
"PgsqlHost" = "localhost"
"PgsqlPort" = "5432"
"PgsqlUser" = "unicorndb"
"PgsqlPass" = "unicorndb"
"PgsqlDb" = "unicorndb"
"PgsqlTable" = "unicorntable"
```
---
db檔案

```mysql
CREATE TABLE IF NOT EXISTS unicorntable (
	id SERIAL PRIMARY KEY,
	requestid VARCHAR(255),
	requestvalue VARCHAR(255),
	hits INT
); 
```

## 考試題目 11/20 

![](https://i.imgur.com/UiMIwqj.png)

1. AWS VPC *1
2. Public Subnet *2 
3. Private Subnet *2 
4. DB Subnet *2
5. Internet Gateway*1
6. Route tables Public*1 DB*1 Private
7. NAT Gateway *1
8. EC2 in private subnet  (WEB) (asg)
10. EC2 in public subnet  → Bastion, for connecting 
12. RDS in DB subnet
13. EFS Share, auto-mounted to EC2
14. mount server.py in EFS and build in WebS
15. WebServer connect db and by server.py show some data
16. change server.py db data for connect
17. high security

command:
---
```bash
pip3 install flask
pip3 install pymysql[]
```
---
https://awstestbucketcc.s3.us-west-1.amazonaws.com/test.py
### sqlfile:
https://awstestbucketcc.s3.us-west-1.amazonaws.com/data.sql

---
nohup python3 test.py &
---

https://www.jinnsblog.com/2018/04/mysql-export-import-db-table.html

ECS待補充

---

## 一些題目

> 实验目的
> 使用Lambda连接EFS
> 
> 实验要求
> 学会Lambda连接EFS
> 
> 实验原理
> Amazon Elastic File System (Amazon EFS) 可提供简单、无服务器、设置即可忘记的弹性文件系统，以与AWS 云服务和本地资源。它可在不中断应用程序的情况下按需扩展到 PB 级，随着添加或删除文件而自动扩展或缩减，无需预置和管理容量，可自适应增长。Amazon EFS 有一个简单的 Web 服务界面，允许您快速方便地创建和配置文件系统。该服务为您管理所有文件存储基础设施，这意味着您可以避免部署、修补和维护复杂文件系统配置的复杂性。
> 
> 实验步骤
> 1、创建一个EFS与接入点
> ![](https://i.imgur.com/qh3hB58.png)
> 
> 创建接入点
> ![](https://i.imgur.com/FfzPxez.png)
> 
> 
> ![](https://i.imgur.com/QeJAxp3.png)
> 
> 
> 然后创建
> 
> 2、创建Lambda使用的角色
> 角色策略
> 
> {
>     "Version": "2012-10-17",
>     "Statement": [
>         {
>             "Effect": "Allow",
>             "Action": [
>                 "logs:CreateLogGroup",
>                 "ec2:CreateNetworkInterface",
>                 "ec2:DescribeNetworkInterfaces",
>                 "ec2:DeleteNetworkInterface",
>                 "logs:CreateLogStream",
>                 "logs:PutLogEvents"
>             ],
>             "Resource": "*"
>         }
>     ]
> }
> 
> 3、创建Lambda函数
> 指定名称myFunction、运行时python3.8、角色选择先前创建的角色
> ![](https://i.imgur.com/3KYZFLT.png)
> 
> 
> 给Lambda配置VPC，确保Lambda能够访问EFS
> ![](https://i.imgur.com/wx75BSv.png)
> 
> 4、为Lambda添加文件系统EFS
> ![](https://i.imgur.com/14KEh5t.png)
> 
> 
> 选择EFS与接入点
> ![](https://i.imgur.com/bk57MeN.png)
> 
> 
> 创建一台EC2，并连接到接入点上创建一个文件
> ![](https://i.imgur.com/F9GBFo0.png)
> 
> 
> 使用Lambda读取
> ![](https://i.imgur.com/qI6WhKw.png)
> 
> 
> ![](https://i.imgur.com/rSbK9uO.png)
> 
> 
> 实验结果
> ![](https://i.imgur.com/FXKzNrs.png)
> 
> ---
> 
> 实验目的
> 为ELB创建一个Alarms
> 
> 实验要求
> 了解Amazon Web Services
> 了解CloudWatch
> 
> 实验原理
> Amazon CloudWatch实时监控您的Amazon Web Services资源以及您在AWS中运行的应用程序。您可以使用CloudWatch收集和跟踪指标，这些指标是我们可衡量的相关资源和应用程序的变量
> 
> 实验步骤
> 1、点击【服务】选择【EC2】，如下：
> image.png
> 
> 2、在EC2左侧导航栏中，点击【负载均衡器】，并选中这个负载均衡器，如下：
> image.png
> 
> 3、在负载均衡器详情页，选择【监控】并点击【创建警报】，如下：
> image.png
> 
> 4、在“创建警报”页，配置以下信息：
> 当【最小值】of【HTTP 5XX】
> 是:>=【3】数量
> 至少【1】个连续周期，时间为【1分钟】
> 警报名称：【ELB-HTTP-5XX】
> 完成以上配置后，点击【创建警报】，如下：
> image.png
> 
> 实验结果
> 创建警报成功
> image.png
> 
> 动手实验 Lambda操作SSM
> 实验目的
> 使用Lambda上传一个参数
> 
> 实验要求
> 了解Amazon Web Services
> 了解无服务器架构
> 了解Python
> 了解AWS SDK for Python
> 准备一个拥有管理员权限的Lambda角色
> 
> 实验原理
> AWS Lambda是一种计算服务，可让您在不配置或管理服务器的情况下运行代码。AWS Lambda仅在需要时执行您的代码并自动扩展，从每天几个请求到每秒数千个。您只需要为您消耗的计算时间付费，当您的代码未运行时不收取任何费用。借助AWS Lambda，您几乎可以为任何类型的应用程序或后端服务运行代码，并且不必进行任何管理。
> 
> AWS systems manager是一个功能集合，可以帮助您自动管理任务，例如收集系统资源清单、应用操作系统（OS）补丁、自动创建Amazon Machine Image （AMI）以及大规模配置操作系统和应用程序。
> 本实验使用Lambda为系统添加一个参数（一些开发场景可能使用）。
> 实验步骤
> 1、点击【服务】，选择【Lambda】，如下：
> 图片1.png
> 2、在Lambda左侧导航窗格中点击【函数】后再点击【创建函数】，如下：
> 图片2.png
> 3、在“创建函数”页，选择【从头开始制作】，如下：
> 图片3.png
> 
> 4、在下方“基本信息”中配置以下信息：
>         函数名称：【systems_lambda】
>         运行语言：【Python3.7】
>         权限：点击【选择或创建执行角色】
>         执行角色：【使用现有角色】
>         角色名称：”ROLE_NAME” ***注意：此角色拥有管理员的权限。
> 完成以上操作后，点击【创建函数】，如下：
> 图片4.png
> 图片4.2.png
> 
> 5、在“函数代码”模块，编写代码。图中代码是上传一个参数，然后参数值打印出来，如下：
> 图片5.png
> 
> 6、代码如下：
> 
> import boto3
> 
> def lambda_handler(event, context):
> 	client = boto3.client('ssm')
> 	response = client.put_parameter(Name='/xc/game/v1',Value='cstor123',Type='String')
> 	response = client.get_parameter(Name='/xc/game/v1')
> 	value_id = response['Parameter']['Value']
> 	print(value_id)
> 	
> 	response = client.delete_parameter(Name='/xc/game/v1')
> 
> 7、编写完成代码后，点击上方菜单栏中的【保存】，然后点击【测试】，如下：
> 图片7.png
> 
> 8、在“配置测试事件”弹窗页中，配置事件的名称【test】，如下：
> 图片8.png
> 
> 9、下拉菜单栏，点击【创建】，如下：
> 图片9.png
> 
> 10、创建完成后，点击【测试】，如下：
> 图片10.png
> 
> 11、显示执行成功，点击【详细信息】以查看详细信息，如下：
> 图片11.png
> 
> 12、在日志输出中，可以看到我们上传到参数的值，如下：
> 图片12.png
> 
> 实验结果
> Lambda执行成功
> 图片13.png
> 
> ---
> 动手实验 启动S3 access logging
> 实验目的
> 在Amazon S3中启用access logging
> 
> 实验要求
> 了解Amazon Web Services
> 了解对象存储
> 了解启用服务器访问日志的作用
> 
> 实验原理
> 默认情况下，Amazon Simple Storage Service（Amazon S3）不会收集服务器访问日志。在您启用日志记录之后，Amazon S3会将源存储桶的访问日志传输到您选择的目标存储桶。目标存储桶必须位于与源存储桶所在的相同AWS区域中且不得具有默认保留周期设置。
> 服务器访问日志记录详细的记录对S3存储桶提出的各种要求。对于许多应用程序而言。，服务器访问日志很有用。
> 
> 实验步骤
> 1、点击【服务】，选择【S3】，如下：
> image.png
> 
> 2、在“存储桶名称”列表中，选择要为其启用服务器访问日志的存储桶名称，如下：
> image.png
> 
> 3、选择【属性】，点击【服务器访问日志】，如下：
> image.png
> 
> 4、点击【启用日志记录】，配置【目标存储桶】与【目标前缀】，完成以上配置后，点击【保存】，如下：
> image.png
> 
> 实验结果
> 为存储桶启用服务器访问日志记录
> image.png
> 
> 
> 动手实验 创建SQS
> 实验目的
> 如何使用 AWS 管理控制台管理队列和消息
> 
> 实验要求
> 了解Amazon Simple Queue Service (Amazon SQS)概念
> 
> 实验原理
> Simple Queue Service (SQS) 提供安全、持久且可用的托管队列，可让您集成和分离分布式软件系统和组件。SQS 提供常见的构造，例如死信队列和成本分配标签。它提供了一个通用 Web 服务 API，并且可通过 AWS 开发工具包支持的任何编程语言访问。
> 
> 实验步骤
> 1.点击【服务】，选择【SQS】，如下：
> 图片1.png
> 
> 2.点击【立即开始使用】；如下：
> 图片2.png
> 
> 3.在【新建队列】面板中，先在下方选择【FIFO队列】，然后在上方输入队列名称【lkr-sqs.fifo】，然后选择【配置队列】如下。
> 注：FIFO队列的名称必须以.fifo后缀结尾：
> ![](https://i.imgur.com/buDGdw2.png)
> 
> 
> 4.在【队列属性】下，保持配置默认，点击【创建队列】；如下：
> ![](https://i.imgur.com/T6UcL8p.png)
> 
> 5.队列已创建
> ![](https://i.imgur.com/TNzuTue.png)
> 
> 
> 6.点击【队列操作】，选择【发送消息】；如下：
> ![](https://i.imgur.com/B6dmIIM.png)
> 
> 
> 7.在【消息正文】中，输入你所要发送的文本，在【消息组ID】中输入：MysqsGroupld1234567890（因为是测试,随机输入即可），在【消息重复数据删除ID】中输入：MysqsDeduplicationld1234567890，最后选择【发送消息】。如下：
> ![](https://i.imgur.com/UDFd352.png)
> 
> 
> 8.【发送消息至lkr-sqs.Fifo】说明已经成功发送到队列中了，选择【关闭】。如下：
> ![](https://i.imgur.com/MbQrqF3.png)
> 
> 
> 9.再选择【队列操作】，点击【查看/删除消息】。如下:
> ![](https://i.imgur.com/KhsnO76.png)
> 
> 
> 10.在【查看/删除lkr-sqs.fiffo中的消息】面板中，选择【开始轮询消息】。如下：
> ![](https://i.imgur.com/0aAQxuD.png)
> 
> 
> 以下示例显示特定于 FIFO 队列的sqs Group ID(消息组 ID)、sqs Deduplication ID (消息重复数据删除 ID)和序号列。如下：
> ![](https://i.imgur.com/1Sr9cDU.png)
> 
> 实验结果
> 可以轮训到刚刚发送的消息。
> ![](https://i.imgur.com/tFg4MY9.png)
> 
> ---
> 
> 动手实验 利用Amazon CloudWatch 搭建无人值守的Apache监控预警平台
> 实验目的
> 利用Amazon CloudWatch 搭建无人值守的Apache监控预警平台
> 
> 实验要求
> 学会使用利用Amazon CloudWatch 搭建无人值守的Apache监控预警平台
> 
> 实验原理
> CloudWatch一直支持用户发布自定义指标来存储、监控自己关心的业务、应用和系统健康状况；AWS最新发布了CloudWatch Plugin for collectd开源项目，该插件整合了collectd强大的收集各种类型统计数据的能力，帮助客户简化了开发收集自定义指标的相关工作，开箱即用地支持发布Apache、Nginx Web服务器应用指标，内存监控指标等监控数据到CloudWatch进行统一存储、展示和预警。
> 
> 实验步骤
> 1、准备一个角色和一台ec2实例
> 角色的策略
> 
> ```
> {
>     "Version": "2012-10-17",
>     "Statement": [
>         {
>             "Sid": "VisualEditor0",
>             "Effect": "Allow",
>             "Action": "cloudwatch:PutMetricData",
>             "Resource": "*"
>         }
>     ]
> }
> ```
> 
> 创建实例时附加上角色
> ![](https://i.imgur.com/ysDd5ma.png)
> 
> 
> 2、登陆到实例上，搭建环境并自定义指标
> 命令1
> 
> `yum update -y && amazon-linux-extras install collectd -y  && systemctl start collectd && yum install -y httpd && yum install -y collectd-apache && wget https://raw.githubusercontent.com/awslabs/collectd-cloudwatch/master/src/setup.py && yum install -y python-pip &&  pip install --ignore-installed requests && chmod +x setup.py && ./setup.py`
> 
> 大致意思是
> 更新升级所有包同时也升级软件和系统内核、安装监控程序、安装监控阿帕奇的插件、下载配置脚本、安装pip、pip安装requests包时忽略报错、运行配置程序
> 
> 除了这一步骤选择2，其余默认
> ![](https://i.imgur.com/hH6ylxN.png)
> 
> 命令2
> 
> `echo -e "LoadPlugin apache\n<Plugin apache>\n  <Instance \"local\">\n    URL \"http://localhost/server-status?auto\"\n  </Instance>\n</Plugin>" >> /etc/collectd.conf && echo -e "<Location /server-status>\n  SetHandler server-status\n  Order deny,allow\n  Deny from all\n  Allow from localhost\n</Location>" >> /etc/httpd/conf/httpd.conf && echo "apache-local-apache_.*" >> /opt/collectd-plugins/cloudwatch/config/whitelist.conf && systemctl start httpd && systemctl restart collectd`
> 
> 大致意思是
> 修改collectd的配置、修改阿帕奇的配置、将apache相关状态指标加入到CloudWatch collectd插件配置的白名单列表、重启服务
> 
> 3、过几分钟后来到CloudWatch控制查看
> ![](https://i.imgur.com/462xBDX.png)
> 
> ![](https://i.imgur.com/nbNWiEa.png)
> 
> 
> 实验结果
> 以下指标写入到了 CloudWatch 自定义指标
> 建立连接的数量、请求的数量、子进程的保持连接的数量、字节数、子进程的读取的数量、子进程的写的数量、子进程空闲的数量、子进程关闭的数量、子进程启动的数量、子进程完成的数量、子进程打开的数量、空闲子进程工作的数量、子进程占用的数量、子进程发送的数量、子进程dns查询的数量
> 
> ![](https://i.imgur.com/T8ZsfTK.png)


## JAM 2021/12/02


### STEP UP SECURITY

> Background
> You've made it, or at least you thought you had. You've spent the last month developing and testing your ML recommendation model. After all that hard work, you've finally built a highly accurate model that is sure to delight your customers and drive engagement with your site. But, when the day arrived to put it in production, you hit an unexpected snag.
> 
> Your ML training pipeline, implemented as an AWS Step Function (jam-ml-training), gives you "Permission Denied" errors. Ted from the security team has helpfully informed you that the cause of the problem is that they have implemented policies that require you to encrypt all resources using a customer-managed KMS key. He mentioned that both the model training (SageMaker Training Step) and the model deployment (SageMaker CreateEndpointConfig) steps would need to have encryption added for the pipeline to work.
> 
> Your Task
> Create a customer-managed key and modify your step function to ensure so that your SageMaker resources use this key when necessary to comply with your company policy. When you have done that, execute your step function to deploy your model!
> 
> Getting Started
> Start out by going to the Step Functions console and find the jam-ml-training State Machine. Go ahead and run it (it does not require an input to run, so you can leave this field blank) and check out the error message you get. Permission denied. Your step function uses the jam-challenge-step-function-execution-role-REGION IAM role. Are there any conditions attached to that role that prevent you from performing your tasks?
> 
> Inventory
> State Machine: jam-ml-training
> IAM Role: jam-challenge-step-function-execution-role-REGION
> Your solution also makes use of Amazon SageMaker, but all of the SageMaker resources are managed by your step function. This means that you do not need to use the SageMaker console to complete this challenge, but your are encouraged to explore the resources that your step function creates to get a better sense of the integration between these two services. You are welcome to inspect the very simple ML training code, but doing so is not necessary to solve the challenge.
> 
> Your step function executes a lambda function that copies SageMaker data into your account for training. This lambda function, jam-copy-resources functions fine as-is. You do not need to modify this function to complete the challenge.
> 
> Services You Should Use
> Key Management Service
> Step Functions
> Identity and Access Management (Read-Only)
> SageMaker (Read-Only)
> Task Validation
> When you've succesfully deployed your model, this challenge will be complete automatically, but, more importantly, you can sleep soundly knowing your data is encrypted at rest. Additionally, you can always check your progress by pressing the "Check my progress" button in the challenge details screen.
> 
> Important: Your model must be "In Service" to complete this challenge. Once you've succesfully run your Step Function, switch to the SageMaker console to check the status of your Endpoint.
> 
> 
> 1. Create a KMS Key
> Open the Key Management Service (KMS) console in your browser
> Select Customer managed keys
> Select Create key
> Ensure that Symmetric is selected and click Next
> Enter "jam-encryption-key" as the Alias and click Next
> On the "Define key administrative permissions" page, don't select anything and click Next
> On the "Define key usage permissions" page, don't select anything and click Next
> Click Finish
> You will be taken to a page listing the key you just created. Click jam-encryption-key to see the details.
> From the General configuration section, find the ARN and copy it to your laptop for later reference. The ARN should be similar to arn:aws:kms:region-name:12345689012:key/random-characters
> 2. Modify your Step Function
> Open the Step Functions console in your browser
> Select State Machines
> Select jam-ml-training
> Select Edit
> In the text window, edit the training job definition to specify encryption for both the training job and model deployment. You can leave the vast majority of the text unchanged (denoted by ...), and only add two lines:
> {
>     ...,
>     "States": {
>         "Copy Resources": {...},
>         "SageMaker Training Step": {
>             ...,
>             "Parameters": {
>                 ...,
>                 "ResourceConfig": {
>                     ...,
>                     "VolumeKmsKeyId": "KMS Key ARN from Step 1"
>                 },
>                 ...
>             },
>             ...
>         },
>         "SageMaker CreateModel": {...},
>         "SageMaker CreateEndpointConfig": {
>             ...,
>             "Parameters": {
>                 ...,
>                 "KmsKeyId": "KMS Key ARN from Step 1"
>             },
>             ...
>         },
>         "SageMaker CreateEndpoint": {...}
>     }
> }
> Click Save
> Click Save anyways
> 3. Run your Step Function
> Click Start execution
> Delete any text in the box labeled "Input"
> Click Start execution
> Follow along with the progress using the Graph Inspector and Execution event history. From the Graph inspector, select any In Progress or Succeeded event to see details on the right. In the resource field, click the link to view details about the SageMaker resource your step function has created.
> Once the step function has succeeded, your ML endpoint is being created, but takes a few minutes to come into service and complete the challenge. To follow along with the progress, navigate to the Amazon SageMaker console.
> Expand the Inference drop down and click Endpoints
> Click jam-sagemaker-endpoint
> Refresh the page until the status is "In Service"
> 



### S3 TIMES TWO ###

> Task 2
> 
> Update the S3 Source role
> 
> Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.
> Choose Roles.
> 
> Search for the source role (LabStack-prewarm-XXXXXXXX) in the filter bar. It will be associated to the s3 service.
> 
> Click the role to navigate to the the policy summary page.
> 
> Choose the Permissions tab and edit the Managed policy with your destination bucket name under the Resources section. You will need to input your bucket name in both the object and bucket sections.
> 
> Click on Review Policy and then click Save changes.
> 
> 
> Fix the Missing action
> 
> Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.
> Choose Roles.
> 
> Search for the source role (LabStack-prewarm-XXXXXXXX) in the filter bar. It will be associated to the s3 service.
> 
> Click the role to navigate to the the policy summary page.
> 
> Choose the Permissions tab and edit the Managed policy actions to add ReplicateObject.
> 
> Click on Review Policy and then click Save changes.



### GET THE SERVERLESS DATABASE, A SERVERLESS CONNECT! ###

> Background
> The front end application issues Select SQL statement on the following tables frequently. The application team have raised concerns that the SQL query response time have been gradually increasing.
> jam.jam1
> jam.jam2
> Based on some initial checks, you have figured out that both the tables are heavily bloated and decided to schedule VACUUM ANALYZE on these tables for every three minutes to automatically clear the bloat.
> 
> Your task
> You will have to enable pg_cron extension using the command below in the database first before scheduling the maintenance jobs. However, there seems to be some issues while enabling it.
> 
> create extension pg_cron;
> You need to resolve the issues to enable the extension successfully and schedule the jobs using following SQL commands:
> 
> SELECT cron.schedule('vacuum-1','*/03 * * * * ', 'VACUUM ANALYZE jam.jam1');
> SELECT cron.schedule('vacuum-2','*/03 * * * * ', 'VACUUM ANALYZE jam.jam2');
> Once the jobs are scheduled, use the SQL select * from cron.job; to get the job configuration details.
> 
> Getting Started
> Open AWS console and navigate to EC2 in services and connect to the EC2 instance using Session manager. To know how to connect using session manager, please refer EC2SesslonManager. Check the output properties tab to get the details of EC2 instance name to which you need to connect.
> 
> Inventory
> Your AWS account is provisioned with:
> 
> Amazon EC2 Instance
> Amazon Aurora PostgreSQL database cluster
> In order to connect to Amazon Aurora PostgreSQL from EC2 Instance, run the following from the Linux EC2 instance to switch the user to ec2-user.
> 
>   sudo su - ec2-user
> The ec2-user bash_profile on your EC2 Instance is already populated with Aurora PostgreSQL database and login details. Hence, just type the command psql and hit enter/return to connect to Amazon Aurora in command line mode and work on the task.
> 
> Task Validation
> Check the status of the job schedule after 3 minutes using SQL select * from cron.job_run_details; from psql command line .Once the status turns SUCCEEDED, you will find a file created in /tmp location on EC2 with name task-1-result. Copy the content and enter the same at the top of this page which says Enter answer here and click Submit Answer to complete the task.


### GETTING TO KNOW YOUR AMAZON AURORA DATABASE

> Your Organisation has an Amazon Aurora for PostgeSQL Database which is being used by your Product Development team. The team has requested your assistance with below requirements related to the database :
>  
>  A read only copy of the Database which can be used to offload the read-only load and provides automatic failover capabilities in case of AZ failure.
>  
>  Performance Insights enabled on the DB instance.
>  
>  A dashboard which captures the number of outstanding read/write requests waiting to access the disk.
> 
> task1 
> 
> Background
> 
> The Product team needs your experties to make the required changes on their existing Database. As the first task you need to find the Aurora instance and its endpoint on the AWS Console.
> 
> Getting Started
> 
> You will see the option "Open AWS console" at the top right hand side of this JAM Challenge window.
> 
> Your Task
> 
> Open the AWS Console and navigate through it to find the Aurora instance and its writer endpoint.
> 
> Inventory
> 
> An RDS instance has been provisioned for you.
> 
> Services You Should use
> 
> AWS RDS
> 
> Task Validation
> 
> Copy the endpoint name and Paste it in the answer box and Click on "Submit Answer" button.
> 
> Make sure you copy paste the complete endpoint name.
> 
> #### task2
> 
> Background
> 
> Now that you know your instance, you need to start making changes requested by your product development team.
> 
> The first change is to create a read-only copy of the existing instance which can be used to offload the read-only requests.
> 
> Getting Started
> 
> Amazon Aurora Databases provides many powerful features, one of which can be used to create a read-only copy of an existing instance which can be used to offload the reads from the primary DB.
> 
> Your Task
> 
> You need to identify the correct feature and make appropriate changes to the existing cluster.
> 
> Inventory
> 
> AWS Aurora DB Instance you identified in Task1.
> 
> Services you should use
> 
> AWS RDS
> 
> Task Validation
> 
> The task will be completed automatically if you have done the required changes correctly.
> 
> You can always click on "Check My Progress" button to see the status of your task.
> 
> task3
> 
> Background
> 
> The Product Development team has requested you to enable performance insights on the DB instance.
> 
> Getting Started
> 
> You may have to some settings on the existing instance
> 
> Your Task
> 
> Modify the existing writer instance and make appropriate changes which can enable performance insights on the instance.
> 
> Inventory
> 
> AWS Aurora DB Instance you identified in Task1.
> 
> Services you should use
> 
> AWS RDS
> 
> Task Validation


> The task will be completed automatically if you have done the required changes correctly.
> 
> 
> task4
> 
> Background
> 
> The team has a requirement to capture the number of outstanding I/Os (read/write requests) waiting to access the disk for the DB Cluster.
> 
> Getting Started
> 
> The AWS/RDS namespace in Cloudwatch collects couple of metrics by default.
> 
> Your Task
> 
> Identify which metric captures the data to meet the above requirement and create a CloudWatch Dashboard with a "single" widget to capture the required information.
> 
> Inventory
> 
> AWS Aurora DB Instance you identified in Task1.
> 
> Services you should use
> 
> AWS CloudWatch
> 
> Task Validation
> 
> Input the name of the dashboard that you create in the answerbox and click on "Submit Answer" Button.
> 
> Note : Make sure only one widget is created under the dashboard with correct metric. If more than one widget is created than the task will not complete.



### DATA MIGRATION AND S3 SECURITY ###

> Background:
> After experiencing multiple outages due to issues in your current data center, you decided to move your servers to AWS. In order to make the migration as quick and seamless as possible, you took a lift and shift strategy when migrating servers. Now that your file server resides in AWS, you would like to move your files to S3 using the AWS DataSync service and then decommission your file server. 
> 
> Your Task:
> As the Cloud Services Engineer for your company, you have been instructed to use AWS DataSync to copy files from the NFS file server to S3. 
> 
> Getting Started:
> The NFS share is called “/share”. Use the S3 bucket that begins with "destination-". Use the role that starts with "DataSync-S3-Jam-Role". The details of the NFS file server instance and the DataSync agent instance can both be found in the EC2 console. Note: When you are creating the task, change Log level to “Do not send logs to CloudWatch” 
> 
> Inventory:
> EC2 instance running DataSync agent
> 
> EC2 instance hosting the NFS share
> 
> S3 Bucket 
> 
> Services You Should Use:
> AWS DataSync
> 
> Task Validation:
> The task will automatically complete once the files have been copied to the S3 Bucket.

### CONNECT DOTS

> Background
> Your company was recently in the news about its quality products with reasonable prices. Sales have grown exponentially due to the publicity. Last week, the team identified an api-key which is used to validate the user request is out of date and needs replacement. While working on this enhancement, the AWS Services within this serverless architecture lost connectivity between them. The CTO wants to fix this quickly as this could damage the companies hard earned reputation and trust. You are the AWS Cloud Architect selected to start investigating the root cause and fix it.
> 
> The initial investigation revealed that an AWS Step Function gets data from an Amazon API Gateway endpoint and stores it in an Amazon Simple Storage Service (S3) bucket. The Amazon API Gateway RESTAPI validates the incoming request and only provides a response after a successful validation. The AWS Lambda function is updated to validate with the new api-key as part of a recent enhancement request. At present, the step function is failing because of a Bad request. Header value does not match. Please provide a valid header.
> 
> As an AWS Cloud Architect, you need to investigate the root cause and bring the application to normalcy.
> 
> Inventory
> To facilitate this task, the following has been setup in this environment.
> 
> An AWS Step Function.
> AWS Lambda Functions.
> An Amazon API Gateway RESTAPI. URL can be found in output properties.
> AWS IAM Roles required for completing this task.
> Amazon Simple Storage Service (S3) bucket. Bucket name can be found in output properties.
> Your Task
> As an AWS Cloud Architect, you need to identify the root causes and fix issues. You need to make sure that all the existing AWS Services are connected and things are back to normal. 
> 
> Getting Started
> Check the Output Properties tab and get to know the AWS services that are used in the application.
> 
> Click on state machine with name Gateway-S3-Connector-State-Machine
> Make sure you are in the region that this challenge is deployed.
> Navigate to Step Functions in AWS Services.
> Select the recent execution from Executions tab.
> Steps to re-run the step function:
> 
> Navigate to Step Functions in AWS Services.
> Make sure you are in the region that this challenge is deployed.
> Click on state machine with name Gateway-S3-Connector-State-Machine
> Select Start Execution.
> Do not change input and click again on Start Execution.
> Architecture Diagram
> 
> 
> 
> Task Validation
> The task gets automatically completed once the AWS Services are connected and the task validation Lambda function can find the required file in Amazon Simple Storage Service (S3) bucket. In addition, you can always check your progress by clicking on Check my progress button in the challenge details screen.

# k8s相關

https://docs.aws.amazon.com/zh_tw/eks/latest/userguide/install-kubectl.html

# ECS架構RUN比賽SERVER(兩層)
![](https://i.imgur.com/xnZUdbz.png)

1. create ec2(要給ECR的Role)
2. install docker
3. start docker
4. create Dockerfile

```
Dockerfile:
    FROM amazonlinux:2      ##使用linux2
    RUN curl -O {serverURL} ##下載server
    RUN chmod +x server     ##給server權限
``` 
5. docker build -t {image_name}.  ##create image
6. docker run -d -p 80:80 being./server ##run server
7. curl localhost ##測試server有沒有run成功，有的話出現TODO: Create a nice looking homepage.
8. docker push {ecr_URL}/{images_name} ##push到ECR上面
9. create cluster，選Networking only，不要用預設給的VPC，所以直接create
10. 到Task Definition，create new Task Definition，選Fargate，TaskRole用預設，system選linux，IAMRole用預設，memory、cpu因為是測試用，選最小的即可
12. 接著add container，輸入name、imageURL(ECR的)、memory:128、port:80、cpu:256、command: ./
(在ENVIORNMENT裡面那個)，好了之後就可以create了
13. 回到Cluster，在Task裡面Run new Task，Type:Fargate，Task Definition:選剛做好的、VPC:選自己創的、Subnet(private)、sg:port要開80
14. 到Services裡面create，type:Fargate、Task Definition:選剛做好的、VPC:選自己創的、Subnet(private)、sg:port要開80、Auto-assign public IP disable、ELB:選自已創的，好了之後就可以CreateService
15. 檢查網頁有沒有RUN成功


# 壓力測試指令:

``` bash

./pew stress -n 20 -r "http://3\.239\.252\.244/calc\?request=(true|false)(\&input=[0-9]{10})"
./pewpew benchmark --rps 1 --duration 2000 -r "http://3\.239\.252\.244/calc\?request=(true|false)(\&input=[0-9]{10})"

./pewpew benchmark --rps 1 --duration 200 -r "http://beingalb-1154160734\.us-east-1\.elb\.amazonaws\.com/calc\?request=(true|false)(\&input=[0-9]{10})"

```


## GameDay Server Binary Test

* [ALB只有一台EC2撐的EndPoint](https://http://beingalb-1154160734.us-east-1.elb.amazonaws.com/)
* [有掛Amazon CDN（CloudFront）](https://d2pk6yimy1854w.cloudfront.net/)
* 範例參數：https://d2pk6yimy1854w.cloudfront.net/calc?request=true&input=SUNhbkhhelVuaWNvcm4%252FLTU0Mzg%253D

## 獨家dockerfile

``` dockerfile

FROM alpine
RUN apk add gcompat
RUN apk add curl
RUN curl -O http://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/gd2015-loadgen/v0.1/server
RUN chmod +x /server

```

## SQL匯入匯出
```
sudo mysqldump --databases cafe_db -u root -p > CafeDbDump.sql
source /usr/bin/CafeDbDump.sql 
```

## 垂直擴展(購買更好的機器) 水平擴展(增加機器的數量)

https://d3pr554kr9efwx.cloudfront.net/


https://termi.us/3v6#id=bcf6cb34-b02b-4bb9-b00e-e81b36b49cca&scheme=termius%20dark&title=3.145.43.147&pwd=5C434E1718A185B832639E3F61F859882E093D67&connectionId=69cf1624-f131-4210-908b-f2a564804ffe


./pewpew benchmark --rps 3 --duration 20000 -r "http://d3pr554kr9efwx\.cloudfront\.net\/calc\?request=(true|false)(\&input=[0-9]{10})"

http://34.96.84.180/

https://termi.us/3v6#id=71158da6-c386-4fcc-b1fe-ccbed88c9aa8&scheme=termius%20dark&title=ec2-107-22-140-101.compute-1.amazonaws.com&pwd=BA316CFD72776D001CC822BDE9489F46038D8D45&connectionId=ecc127e9-3fc7-4a7d-bec9-d480ff4a87be

## SQS訊息傳送順序
1.Standard queues 
EX:遊樂園雲霄飛車一台6個人，缺了3人，服務人員會尋找剛好人數的遊客補滿雲霄飛車\
2.FIFO 
EX:先到的餐點先給
## SQS訊息傳送方式
1.Dead-letter queue support : 訊息傳送失敗，重新傳送(排隊)\
2.Visibility timeout : 訊息傳送失敗，一定時間後刪除\
3.Long polling : 等到有訊息，或是timeout才回傳結果\
## SQS總結
6.適合使用SQS:服務與服務之間交流、是否觸發\
7.不適合使用SQS:特定訊息(改使用AWS MQ)、大訊息量\
## 好的架構
1.卓越營運\
2.安全性\
3.可靠性\
4.效能效率最佳化\
5.成本最佳化\
6.永續發展
## 去年全國賽題目
1.基本ECS架構
![](https://i.imgur.com/LANf6Ml.png)
2.給一個架構，讓你修好(CTF)
![](https://i.imgur.com/DtmKSS6.png)
3.架構設計(15分鐘想，15分鐘報告)
![](https://i.imgur.com/e0YXDeA.png)
## 練習題
![](https://i.imgur.com/VVnmw8V.png)
ANS:D，long polling 會等到有訊息進時，再發送，不會拉到空佇列
## 微服務定義、特點
單一的Application拆開來變成多個獨立Application
1.去中心化\
2.獨立的\
3.多語言\
4.專門的\
5.黑盒子(Application彼此不知道彼此之間在幹嘛)\
6.你建構的，只有你會知道
## 容器
包含你的應用程式code、運行系統、依賴、配置
![](https://i.imgur.com/wCrdAlW.png)
## AWS serverless服務
![](https://i.imgur.com/XoxyWPC.png)
## 使用lambda實施無伺服器架構
![](https://i.imgur.com/t2M8ts4.png)
1.創建lambda function
Runtime: Python 3.7
2.選擇IAM role
Existing role: Lambda-Load-Inventory-Role(讓Lambda可以訪問s3)
3.貼上source code，之後deploy
```
# Load-Inventory Lambda function
#
# This function is triggered by an object being created in an Amazon S3 bucket.
# The file is downloaded and each line is inserted into a DynamoDB table.
import json, urllib, boto3, csv
# Connect to S3 and DynamoDB
s3 = boto3.resource('s3')
dynamodb = boto3.resource('dynamodb')
# Connect to the DynamoDB tables
inventoryTable = dynamodb.Table('Inventory');
# This handler is run every time the Lambda function is triggered
def lambda_handler(event, context):
  # Show the incoming event in the debug log
  print("Event received by Lambda function: " + json.dumps(event, indent=2))
  # Get the bucket and object key from the Event
  bucket = event['Records'][0]['s3']['bucket']['name']
  key = urllib.parse.unquote_plus(event['Records'][0]['s3']['object']['key'])
  localFilename = '/tmp/inventory.txt'
  # Download the file from S3 to the local filesystem
  try:
    s3.meta.client.download_file(bucket, key, localFilename)
  except Exception as e:
    print(e)
    print('Error getting object {} from bucket {}. Make sure they exist and your bucket is in the same region as this function.'.format(key, bucket))
    raise e
  # Read the Inventory CSV file
  with open(localFilename) as csvfile:
    reader = csv.DictReader(csvfile, delimiter=',')
    # Read each row in the file
    rowCount = 0
    for row in reader:
      rowCount += 1
      # Show the row in the debug log
      print(row['store'], row['item'], row['count'])
      try:
        # Insert Store, Item and Count into the Inventory table
        inventoryTable.put_item(
          Item={
            'Store':  row['store'],
            'Item':   row['item'],
            'Count':  int(row['count'])})
      except Exception as e:
         print(e)
         print("Unable to insert data into DynamoDB table".format(e))
    # Finished!
    return "%d counts inserted" % rowCount
```
4.創建bucket桶\
5.新增事件通知(讓S3創建東西時觸發Lambda)\
6.上傳檔案\
7.創建SNS，當缺貨時發電子郵件\
8.創建測試用Lambda，source code:
```
# Stock Check Lambda function
#
# This function is triggered when values are inserted into the Inventory DynamoDB table.
# Inventory counts are checked and if an item is out of stock, a notification is sent to an SNS Topic.
import json, boto3
# This handler is run every time the Lambda function is triggered
def lambda_handler(event, context):
  # Show the incoming event in the debug log
  print("Event received by Lambda function: " + json.dumps(event, indent=2))
  # For each inventory item added, check if the count is zero
  for record in event['Records']:
    newImage = record['dynamodb'].get('NewImage', None)
    if newImage:      
      count = int(record['dynamodb']['NewImage']['Count']['N'])  
      if count == 0:
        store = record['dynamodb']['NewImage']['Store']['S']
        item  = record['dynamodb']['NewImage']['Item']['S']  
        # Construct message to be sent
        message = store + ' is out of stock of ' + item
        print(message)  
        # Connect to SNS
        sns = boto3.client('sns')
        alertTopic = 'NoStock'
        snsTopicArn = [t['TopicArn'] for t in sns.list_topics()['Topics']
                        if t['TopicArn'].lower().endswith(':' + alertTopic.lower())][0]  
        # Send message to SNS
        sns.publish(
          TopicArn=snsTopicArn,
          Message=message,
          Subject='Inventory Alert!',
          MessageStructure='raw'
        )
  # Finished!
  return 'Successfully processed {} records.'.format(len(event['Records']))
```
9.Add trigger\
Select a trigger: DynamoDB\
DynamoDB Table: Inventory\
10.complete!!

