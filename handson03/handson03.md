# ハンズオン03  
- スケーラビリティのあるブログサービスを構成する。   
ELBにAuto Scalingグループを紐づけてEC2を最大4最小2の範囲でスケーリングさせる。  
Auto Scaling全体のCPU使用率（70％以上）を監視するアラームを紐づけて、EC2に負荷をかけスケーリングすることを確認する。  

構成図  

![koiseizu](./img03/handson03.drawio.png) 

- 起動テンプレートの作成  
前回作成したEC2を起動し、EC2からテンプレートを作成する。  
テンプレートの作成の際、マシンイメージ（AMI）は前回使用した自分のAMIを使用する。  

![template01](./img03/template.png)  

![template02](./img03/template2.png)  

- auto scalingグループの作成  

![auto01](./img03/auto1.png)  
![auto02](./img03/auto2.png)  
![auto03](./img03/auto3.png)  
![auto04](./img03/auto4.png)  

- CloudWatchアラームの作成  
CPU使用率が70％以上の時に通知が登録されたメールアドレスに来るようにする。  
一度CloudWatchに関しては授業で[課題](https://github.com/shio0727/Kadaiyou/blob/main/lecture06/lecture06.md)
で取り扱っている為割愛する。  
メトリクスはEC2→AutoScalingグループ別→CPUUtilizationを選択する  

![alarm](./img03/alarm.png)   

- スケーリングポリシーの作成  
CloudWatchアラームをスケーリングポリシーに連携する

![scalingpolicy](./img03/scalingpolicy.png)  

- 動作確認  
SSH接続したEC2に負荷をかける。 

```bash:title  
$ yes >> /dev/null &  
```  
![fuka](./img03/fuka.png) 

EC2が増加している事をlogで確認する。
![log](./img03/EC2tuikalog.png)  





