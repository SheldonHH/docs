Zeus Getting Started
====================

## Overview
zeus-cmd is an Extensible command line tool. SDK extensions come packaged in "boxes".

## Boxes

* EOSIO dApp development support
* DAPP Services support
* coldtoken  - vRAM based eosio.token https://github.com/liquidapps-io/zeus-coldtoken-sample
* deepfreeze - vRAM based cold storage contract for multiple tokens https://github.com/liquidapps-io/deepfreeze
* vgrab      - vRAM based airgrab for eosio.token https://github.com/liquidapps-io/vgrab

Getting started
--------------

### Prerequisites:

* nodejs == 10.x (nvm recommended)
* curl
* nodeos 

Recommended (otherwise falling back to docker)
* [eosio.cdt v1.6.1](https://github.com/EOSIO/eosio.cdt/releases/tag/v1.6.1)
* [eosio v1.7.1](https://github.com/EOSIO/eos/releases/tag/v1.7.1)

### Install Zeus

```bash
npm install -g @liquidapps/zeus-cmd
```

#### Notes regarding docker on mac:
Recommended version: 18.06.1-ce-mac73

### Upgrade

```bash
npm update -g @liquidapps/zeus-cmd
```

### Test
```bash
zeus unbox helloworld
cd helloworld
zeus test
```

### Other Options
```bash
zeus compile #compile sample contracts
zeus migrate #migrate sample contracts (deploy to local eos.node)
```

### Notes regarding permissions errors:
Recommend using Node Version Manager (nvm)
```bash
sudo apt install curl
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
exec bash
nvm install 10
nvm use 10
```
Or you can try the following:
```bash
sudo groupadd docker
sudo usermod -aG docker $USER

#If still getting error:
sudo chmod 666 /var/run/docker.sock
```

### Usage inside a project
```bash
zeus --help 
```

#### List Boxes
```bash
zeus list-boxes
```

## Project structure
### Directory structure
```
    extensions/
    contracts/
    frontends/
    models/
    test/
    migrations/
    utils/
    services/
    zeus-box.json
    zeus-config.js
```
### zeus-box.json
```
    {
      "ignore": [
        "README.md"
      ],
      "commands": {
        "Compile contracts": "zeus compile",
        "Migrate contracts": "zeus migrate",
        "Test contracts": "zeus test"
      },
      "install":{
          "npm": {
              
          }
      },
      "hooks": {
        "post-unpack": "echo hello"
      }
    }
```

### zeus-config.js
```
    module.exports = {
        defaultArgs:{
          chain:"eos",
          network:"development"
        },
        chains:{
            eos:{
                networks: {
                    development: {
                        host: "localhost",
                        port: 7545,
                        network_id: "*", // Match any network id
                        secured: false
                    },
                    jungle: {
                        host: "localhost",
                        port: 7545,
                        network_id: "*", // Match any network id
                        secured: false
                    },
                    mainnet:{
                        host: "localhost",
                        port: 7545,
                        network_id: "*", // Match any network id
                        secured: false
                    }
                }
            }
        }
    };
```
