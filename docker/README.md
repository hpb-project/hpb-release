##### Tip
hpb docker image only can be used to make a syncnode, you can't use it to make a pre-node.
##### install hpb image
docker load < docker-ghpb-v1.0.3.1.tar.gz
and `docker image ls ` check load successed.

##### make new hpb sync node
create a new dictionary as datadir for syncnode and then run the docker.
```shell
mkdir /path/to/syncnode
wget https://raw.githubusercontent.com/hpb-project/hpb-release/master/config/gensis.json -P /path/to/syncnode
docker run -it --privileged=true  --rm -v /path/to/syncnode/:/root/node/ --name ghpbinit ghpb:v1.0.3.1 --datadir /root/node/data init /root/node/gensis.json

docker run -itd --privileged=true --restart=always -v /path/to/syncnode/:/root/node/ -p 8545:8545 -p 30303:30303 --name ghpb1 ghpb:v1.0.3.1 --datadir /root/node/data --networkid 100 --verbosity 3 --rpc --rpcaddr 0.0.0.0 --rpcapi hpb,web3,admin,txpool,debug,personal,net,miner,prometheus --nodetype synnode console
```
##### enter ghpb console
	docker attach ghpb1 

##### exit ghpb console
    Press Crl+p+q on the keyboard.

##### lookup logs
	docker logs -f ghpb1
