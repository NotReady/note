# AWS

## VPC
***
### IGW
***
Internet GatewayもNAT変換している。
* InternetGateway   
ElasticIPを設定したインスタンスのCIDRと1対1で変換
* NatGateway(1:*変換)  
TCPポートで1対多のセッション管理をしているため、アウトバウンド発の流入を抑止する。

> https://webcache.googleusercontent.com/search?q=cache:xD8OTGFZUxMJ:https://milestone-of-se.nesuke.com/sv-advanced/aws/internet-nat-gateway/+&cd=2&hl=ja&ct=clnk&gl=jp&client=firefox-b-d