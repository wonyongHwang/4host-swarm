# 4host-swarm
Deploy multi-host First Network (using Fabric v2.5)

Source of article: https://medium.com/@kctheservant/multi-host-deployment-for-first-network-hyperledger-fabric-v2-273b794ff3d

### Below I've summarized the parts of the link above that need to be added or modified. !!!


## 🧱 PreRequisites
Fabric 2.5 binaries and samples should be intalled.
```
curl -sSLO https://raw.githubusercontent.com/hyperledger/fabric/main/scripts/install-fabric.sh && chmod +x install-fabric.sh
./install-fabric.sh
```
https://hyperledger-fabric.readthedocs.io/en/release-2.5/install.html

## 🧱 Generate a Certificate using cryptogen
#### * at source root directory 
```
../bin/cryptogen generate --config=./crypto-config.yaml
```
## 🧱 Generate a Genesis Block and Channel Configuration using configtxgen
#### * at source root directory 
```
../bin/configtxgen -profile SampleMultiNodeEtcdRaft -channelID system-channel -outputBlock ./channel-artifacts/genesis.block
../bin/configtxgen -profile TwoOrgsChannel -outputCreateChannelTx ./channel-artifacts/channel.tx -channelID mychannel
../bin/configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx -channelID mychannel -asOrg Org1MSP
../bin/configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx -channelID mychannel -asOrg Org2MSP
```
## 🧱 ChainCode Packaging
at host1 :
```
docker exec cli peer lifecycle chaincode package fabcar.tar.gz --path /opt/gopath/src/github.com/chaincode/fabcar/go --label fabcar_1
```



