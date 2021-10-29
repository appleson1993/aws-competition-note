# 雲端小組筆記 

友情鏈結: 
https://hackmd.io/OFAv7nEzSN21wJAvXl0nsQ

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

------

## 常用記錄檔

#!/bin/bash
sudo -i
sudo amazon-linux-extras install nginx1.12 -y
sudo amazon-linux-extras install php7.4 -y
sudo systemctl enable php-fpm.service 
sudo systemctl start php-fpm
sudo systemctl enable nginx
sudo systemctl start nginx
sudo echo "<?php phpinfo(); ?>" > /usr/share/nginx/html/index.php

一鍵指令

sudo amazon-linux-extras install nginx1.12 -y &&
sudo systemctl enable nginx &&
sudo systemctl start nginx


## nginx 依照nginx.conf內容啟動
sudo nginx -c /etc/nginx/nginx.conf



> 查MYSQL密碼 sudo grep 'password' /var/log/mysqld.log

 jam platform
 https://digitalcloud.training/certification-training/aws-solutions-architect-associate/
 
## 一些常用指令
 -------

在linux上進行ssh連線
ssh -i key ec2-user@ip
追蹤路由器
traceroute
> []
https://reurl.cc/8y4M3y

啟動自動安裝httpd指令

```
#!/bin/bash
sudo yum install -y httpd
sudo echo "<h1><b>Welcome to my world 2</b></h1>" > /var/www/html/index.html
sudo service httpd start
sudo chkconfig httpd on
```


```
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


```
df -h
```
- 記得改EFS SG allow port 2049 from EC2 SG
- EC2則不用改，因為Outbond流量是1-65535。


CPU壓力測試指令:
```
for i in `seq 1 $(cat /proc/cpuinfo |grep "physical id" |wc -l)`; do dd if=/dev/zero of=/dev/null & done
```
查看CPU以及運行工作指令:

```
yum install htop

htop
```
https://www.itread01.com/content/1546701868.html
wget http://pyropus.ca/software/memtester/old-versions/memtester-4.2.2.tar.gz
tar zxvf memtester-4.2.2.tar.gz cd memtester-4.2.2 make && make install


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

```
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

```
#!/bin/bash
sudo -i
yum install -y docker
systemctl enable docker.service
systemctl enable docker.socket
systemctl start docker.service
systemcrl start docker.socket
```

- 記住別用aws在創instance時給的掛載功能，一定要自己打，坑爹玩意兒！



## 啟用 Nginx Status 的設定
sudo nano /etc/nginx/nginx.conf
在nginx.conf裡面改(寫在server裡面)
```
server {
...
    location /nginx_status {
        stub_status on;
    }
}
```



## useful姿勢：讓Auto Scaling 的Web檔案可以同時一起更新
- EC2中掛載EFS雲盤
- 重新開機之後一樣能自動掛載
- 要到 VPC 裡面去開 DNS 解析，才可以連得上去
```
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
https://dywang.csie.cyut.edu.tw/moodle23/dywang/linuxSystem/node46.htm




## s3 bucket policies

```
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
```
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
```
#!/bin/bash
sudo -i
cd /
wget {s3 bucket URL}
chmod +x apache.sh
./apache.sh
```

## fish 套件 (可以題字)
```
sudo amazon-linux-extras epel
sudo yum install fish
```

## Redis 安裝+連線
```
sudo yum install gcc (編譯器)
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make
src/redis-cli -c -h {Redis End point} 括號不要+
```
![](https://i.imgur.com/XUfHgwg.png)

## shell script 自動安裝apache + 自動掛載EFS + 設定檔案目錄
```
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
```
1.到AWS IAM 建立 Roles
2.選擇Ec2，按下一步
3.搜尋S3 選擇AmazonS3FullAccess (也可以create policy)
4.打role name 完成創立
5.將Ec2套用IAM Roles
6.將s3 bucket policy 設定為允許存放物體(PutObject,GetObject) (比賽中可以使用官方文檔做編輯)
ex:
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
7.到EC2中，打上(aws s3 cp "你要上傳的東西" s3://"s3名稱")
ex:aws s3 cp apache.sh s3://beings3   <--cp是複製 mv是移動
8.到S3中檢查是否上傳完畢
```

## CloudFont Origin requset policy CDN規則設置
```
CloudFont > policy > origin request > create origin request policy
Headers > all viewer headers
Query strings > all
Cookies > all
```
## game day binaray

比賽server:
http://s3.amazonaws.com/ee-assets-prod-us-east-1/modules/gd2015-loadgen/v0.1/server


https://d102pi46qqn7m7.cloudfront.net/



https://abukkithi.s3.amazonaws.com/http_status_test.zip
比賽server:http://ec2-52-55-182-143.compute-1.amazonaws.com/http_status_test/


server-bang.linux

http://ee-assets-prod-us-east-1.s3.amazonaws.com/modules/gd2015-loadgen/v0.1/server

http://34.207.243.203/



## jam


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
       "mainSteps":[
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



 docker kill [OPTIONS] CONTAINER [CONTAINER...]

 docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
 
 ## ECS run binary
```

Create Dockerfile:
    FROM amazonlinux:2
RUN yum install httpd -y
RUN systemctl enable httpd
RUN curl -O https://beings3.s3.amazonaws.com/server
RUN chmod +x server

docker build -t {images_name}. ## 創建docker images
docker images ## 檢查是否有create成功
docker run -d -t -p 8080:80 being ./server 
docker ps ## 檢查container是否RUN成功
---->Preview Running Application ##測試binary是否成功啟動

```

小提醒：

要先push到aws ecr裏面
然後用舊版控制台操作

![](https://i.imgur.com/c9Wm9BN.png)

開始使用比較簡單

![](https://i.imgur.com/2Zp6QGs.png)


https://ithelp.ithome.com.tw/articles/10190824