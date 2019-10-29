# SES (Amazon Simple Email Service)
E メール送信のサービス。  
SMTP プロトコルを利用して、あるいはプログラムから直接 E メールを送信する際に利用する。  
E メールを受信し S3 に保存することも可能。  

## SES の特徴
高い配信性能。
- 送信時にウイルスやマルウェアを検出してブロックする機能  
- 送信の成功数や拒否された数を統計的に処理し、配信不能や苦情を管理する機能  
- Sender Policy Fremework や DomainKeys Identified Mail といった認証機能  

利用者への制約  
- Bounce Mail の比率を 5% 以下に保ち続ける  
- 苦情を防ぐ (0.1% 未満)  
- 悪意のあるコンテンツを送らない  
