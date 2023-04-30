# CloudFormation
CloudFormation Template
【構成図】<br>
※「template-public.txt」を使用して、<br>
  EC2をPrivate subnetに展開した場合の構成図です。
![configuration.png](configuration.png)

【工夫点】  
・EC2を展開するサブネットを選べるように、２種類のテンプレートを作成。  
  EC2をプライベートサブネットへ展開することで、EC2を外部アクセスから遮断できると考えたが、NatGateWayの料金が膨らむことから、EC2をパブリックサブネットに展開するテンプレートも作成した。  
  EC2をパブリックサブネットに展開するテンプレートでは、以下を使用し、セキュリティ面を強化した。  
  ①セキュリティグループを使用して、ALB、RDS以外からのアクセスを拒否。
  ②ALBログを収集し、クライアントIPアドレスをS3へ記録。  
  
・ALBへのアクセスをCloudFrontからのみに設定。マネージドプレフィックスを使用。  
  
・RDSパスワードやRDSユーザー名を「Secret Manager」を使用して、動的参照。