#ハンズオン01  
- 基本的なブログサービスの構築（シングル構成）  
構成図  
![kouseizu]()

※環境構築部分は[課題](https://github.com/shio0727/Kadaiyou/blob/main/lecture04.md)と重複する為割愛する  

- WordPressのインストール 


```bash:title
$ sudo su -  
#理者権限に切り替える

$ yum -y update  
#EC2のパッケージの状態を最新版にする

$ amazon-linux-extras install php7.2 -y  
$ yum -y install mysql httpd php-mbstring php-xml gd php-gd  
#必要なパッケージをインストールする  

$ systemctl enable httpd.service  
#再起動後も自動で起動するようにする  
$ systemctl start httpd.service  
#起動する  

$ wget http://ja.wordpress.org/latest-ja.tar.gz ~/  
#WordPressをダウンロードする  
# $ ll で確認  
$ tar zxvf ~/latest-ja.tar.gz  
#圧縮しているファイルを元に戻す  

$ cp -r ~/wordpress/* /var/www/html/  
#WordPressにあるファイルを/var/www/html/ ディレクトリごとコピーする。　　
$ chown apache:apache -R /var/www/html  
#権限変更を行う  

```  
- プラウザから初期設定を行う  
```bash:title  
データベース名：WordPress  
ユーザー名：WordPress  
パスワード名：RDSのPW  
データベースのホスト：RDSのエンドポイント  

![]()