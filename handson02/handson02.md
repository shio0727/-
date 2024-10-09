# ハンズオン02  
- 基本的なブログサービスの構築（冗長構成）  
構成図  
![kouseizu](./img/)  

- 冗長化構成とは？  
EC2一つでは何らかの障害が発生した際にサービス全体が停止してしまう。それを防ぐため、負荷が分散できるようにサーバーを増やした構成の事  

- Webサーバーのindex.phpを編集しEC2を識別できるようにする  
```bash:title  
$ sudo su -
#rootに移動  
$ cd /var/www/html　　
$ vi index.php　　
echo '<p>Web Server 1</p>';  
#追加する  
```  
![1](./img/) 
- EC2のAMIを取得  
![AMI](./img/)  
- AMIからEC2を起動  
![AMI](./img/)  
起動したのちに二つ目のWebサーバーのindex.phpを編集して識別できるように”２”と表示させる。  
![2](./img/) 
- ELBの作成  
![ELB](./img/)  
- DBの情報の更新  
```bash:title  
$ mysql -h database-1.xxxxxxxxxxxxxxxxxxxxxxx.ap-northeast-1.rds.amazonaws.com -u wordpress -p  
#RDSにログイン  
$ USE wordpress  
$ SELECT * FROM wp_options WHERE option_name IN ('siteurl', 'home');  
$ UPDATE wp_options SET option_value = 'http://xx.xx.xx.xx' WHERE option_name IN ('siteurl', 'home');  
#EC2のパブリックIPだった部分をELBのDNS名に変更する。  
```
- WebサーバーのセキュリティグループをELBからの通信のみにする  
![sg](./img/)  
- RDSをマルチAZ構成に冗長化  
RDSの変更からマルチAZ構成に変更する。フェイルオーバーで再起動  
![sg](./img/)