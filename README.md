# Kubernetes 部署iotex-core指导
## 先决条件
1. 当前已经拥有k8s集群，kubectl 已经连接至对应的Cluster

2. 拥有一个静态外部IP地址，没有的话，可以相应云提供商处申请

## 创建configmap
1. 从[iotex-testnet](https://github.com/iotexproject/iotex-testnet)处拉取`config.yaml`和`genesis.yaml`

2. 替换`externalHost`和`producerPrivKey`，配置好你的`config.yaml`

3. 创建configmap  
```
kubectl create configmap iotex-mainnet-config	--from-file=your-path/config.yaml --from-file=your-path/genesis.yaml
```

## 创建`iotex-service`服务

1. 下载本仓库目录下的`iotex-k8s-config.yaml`文件

2. 修改`iotex-k8s-config.yaml`,修改`loadBalancerIP`字段为你的静态IP地址,修改`image`字段为对应的`iotex-core`镜像仓库

3. 创建服务
```
kubectl create -f iotex-k8s-config.yaml
```

4. 等服务启动，查看服务命令
```
kubectl get svc iotex-service
```

