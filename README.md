# oneshot-softether-vpn

Softether VPN で L2TP over IPSec サーバーを構築する AWS CloudFormation テンプレートです。EC2 インスタンスだけでなく、必要なリソースを一通り作成することができます。

## 使い方

`aws cli` 、又は、AWS マネジメントコンソールで `template.yml` からスタックを作成します。

```
$ aws cloudformation create-stack --stack-name oneshot-softether-vpn --template-body file://$(pwd)/template.yml \
--parameters ParameterKey=VPNPSK,ParameterValue=vpns \
ParameterKey=VPNServerPassword,ParameterValue=ServerPassword \
ParameterKey=VPNUser,ParameterValue=user \
ParameterKey=VPNUserPassword,ParameterValue=password \
ParameterKey=KeyPair,ParameterValue=aws-keypair1 \
--capabilities CAPABILITY_IAM
```

以下のパラメータを指定する必要があります。ここで指定したパラメータが Softether VPN に設定されます。

- `VPNServerPassword`
  - Softether VPN の管理パスワード。
- `VPNUser`
  - VPN の接続ユーザー。
- `VPNUserPassword`
  - `VPNUser` のパスワード。
- `VPNPSK`
  - VPN の事前共有鍵。
- `KeyPair`
  - Softether VPN をインストールする EC2 インスタンスに設定する EC2 Key Pair。

デプロイが成功すると、`Outputs` セクションに出力される IP に対して L2TP over IPSec 接続ができるようになります。