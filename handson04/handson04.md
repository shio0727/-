# ハンズオン04  
- ## 独自ドメインを設定する、障害時はSORRYページへ通信を流す  
他社サイトで取得したドメインのネームサーバーを書き換え、ドメインを紐づける  
フェイルオーバールーティングに設定をし直す  

- ### ドメインの取得  
[お名前ドットコム](https://www.onamae.com/server/)で無料ドメインを取得する  


- ### Route 53 ホストゾーンの作成  
![host](./img04/host.png)  
![hostzone](./img04/hostzonesakusei.png)  
![record1](./img04/record1.png)  
- ### ネームサーバーの変更(お名前ドットコムでの操作)  
Route 53 で発行したネームサーバーを使用する。  
![onamae](./img04/onamae.png)  
- ### 取得したドメインでアクセスできるように設定する  
シンプルルーティングを選択し、Route 53でレコードを作っていく
![record2](./img04/record2.png)  
- ### フェイルオーバールーティングの設定を行う。  
S3バケットを製作する（名前をドメインの名前と揃える必要がある）  
![S3](./img04/S3.png)  
ブロックパブリックアクセスを無効にする  
![pub](./img04/pub.png)  
画像とhtmlファイルをS3バケットの中に入れる
![gazou](./img04/gazou.png)  
S3のプロパティの一番下にある静的ウェブサイトホスティングを編集  
![seitekiweb1](./img04/seitekiweb1.png)  
![seitekiweb2](./img04/seitekiweb2.png)  
アクセス許可のメニューからバケットポリシー[](https://docs.aws.amazon.com/ja_jp/AmazonS3/latest/user-guide/static-website-hosting.html)を設定する  
![policy](./img04/policy.png)  
先ほどシンプルルーティングで設定したレコードをフェイルオーバールーティングに変え、プライマリを選択する。  
セカンダリのものも作成する。  
![second](./img04/second.png)  
![EL-P](./img04/EL-P.png)  
![EL-S](./img04/EL-S.png) 
