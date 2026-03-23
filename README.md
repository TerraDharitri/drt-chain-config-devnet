<div style="text-align:center">
  <img
  src="https://raw.githubusercontent.com/TerraDharitri/drt-go-chain/main/dharitri-logo.svg"
  alt="DharitrI">
</div>
<br>

<br>

[![](https://img.shields.io/badge/made%20by-DharitrI-blue.svg?style=flat-square)](http://dharitri.org/)
[![](https://img.shields.io/badge/project-DharitrI%20Devnet-blue.svg?style=flat-square)](http://dharitri.org/)

# drt-chain-config-devnet for the official devnet (developer testnet)

DharitrI devnet configuration files used in conjunction with drt-go-chain project. 
For more info how to connect to the devnet, please check [here](https://docs.dharitri.org/validators/nodes-scripts/config-scripts/)

## run an DharitrI observer/validator with docker

### build docker image
```docker image build . -t chain-devnet-local -f ./docker/Dockerfile```

### run node with docker
```
CONFIG_FOLDER=path/to/folder/with/pem/file
docker run --mount type=bind,source=${CONFIG_FOLDER}/,destination=/data chain-devnet-local --validator-key-pem-file="/data/validatorKey.pem" --log-level *:DEBUG
```

### files not to delete
````
'.git'
'.github'
'docker'
'full-archive-seeders'
'main-seeders'
'scripts'
'binaryVersion'
'goVersion'
'proxyVersion'
````

## all others are auto-generated




