<div style="text-align:center">
  <img
  src="https://raw.githubusercontent.com/dharitri/drt-go-chain/master/dharitri-logo.svg"
  alt="Dharitri">
</div>
<br>

<br>

[![](https://img.shields.io/badge/made%20by-Dharitri-blue.svg?style=flat-square)](http://dharitri.org/)
[![](https://img.shields.io/badge/project-Dharitri%20Devnet-blue.svg?style=flat-square)](http://dharitri.org/)

# drt-chain-config-devnet for the official devnet (developer testnet)

Dharitri devnet configuration files used in conjunction with drt-go-chain project. 
For more info how to connect to the devnet, please check [here](https://docs.dharitri.org/validators/nodes-scripts/config-scripts/)

## run an Dharitri observer/validator with docker

### build docker image
```docker image build . -t chain-devnet-local -f ./docker/Dockerfile```

### run node with docker
```
CONFIG_FOLDER=/home/dharitri/workspace/Devnet/drt-chain-config-devnet
sudo docker run --mount type=bind,source=${CONFIG_FOLDER}/,destination=/data chain-devnet-local --validator-key-pem-file="/data/validatorKey.pem" --log-level *:DEBUG

```