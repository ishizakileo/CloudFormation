# CloudFormation

【構成図】<br>
※「template-public.txt」を使用して、EC2をPrivate subnetに展開した場合の構成図。
![configuration.png](configuration.png)

【工夫点】  
・EC2を展開するサブネットを選べるように、２種類のテンプレートを作成。  
  EC2をプライベートサブネットへ展開することで、EC2を外部アクセスから遮断できると考えたが、NatGateWayの料金が膨らむことから、EC2をパブリックサブネットに展開するテンプレートを作成。  
  
・セキュリティグループを使用したアクセス制限。  
　各リソースのアクセス許可設定は以下です。  
  ALB: Cloudfront, EC2  
  EC2: ALB, RDS
  RDS: EC2
  
・ALBログを収集し、クライアントIPアドレスをS3へ記録。  
  
・ALBへのアクセスをCloudFrontからのみに設定。マネージドプレフィックスを使用。  
  
・RDSパスワードやRDSユーザー名を「Secret Manager」を使用して、動的参照。