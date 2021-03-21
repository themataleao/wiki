NOTE: Please keep in mind we regularly update our testnet and potentially wipe out existing history

## Download JAR

Currently running **v0.7.1** ([download](https://github.com/alephium/alephium/releases/download/v0.7.1/alephium-0.7.1.jar))

Block explorer: [http://devnet.alephium.org](http://devnet.alephium.org)

## Configure your node

Before starting the node, you should set the following content in the file `~/.alephium/user.conf`:

    alephium.network.network-type = "testnet"
    alephium.discovery.bootstrap = ["18.218.41.122:9973", "3.17.57.22:9973"]

NOTE: If you are upgrading from a previous release, please ensure `~/.alephium` is clean of any `db-*` folders

## Start your node
You are now ready to start your node using the JAR you downloaded earlier.

    java -jar alephium-v0.7.0.jar

If running on Unix system, please ensure the system is providing enough entropy or setup an agent like `haveged`.

NOTE: The log files will be stored in `~/.alephium/logs`

## Getting Started

### Tools

You can use Swagger (or any other openapi clients). We recommand Swagger as it provide the most straightforward UX.

### Swagger

You can directly open Swagger UI through `http://localhost:12973/docs`.

Alternatively, you can also import the API using "File - Import file", 
when prompted select the file `openapi.yaml` which you can [download](https://github.com/alephium/alephium/raw/master/api/src/main/resources/openapi.yaml) from our repository.

### Create a new wallet

You can create a new wallet by doing a POST with the following data on `/wallets`.

    {
        "password": "123456",
        "walletName": "foo",
        "mnemonicPassphrase": "",
        "mnemonicSize": "24"
    }

The server must answer successfully giving you our new wallet mnemonic.

    {
        "walletName": "foo",
        "mnemonic": "laptop tattoo torch range exclude fuel bike menu just churn then busy century select cactus across other merge vivid alarm asset genius mountain transfer"
    }

Fetch your new wallet address by GET `/wallets/foo/addresses`.

    {
        "activeAddress": "T15Egvi9uHA1Jj9hxMJFcuPJ9xo6VTDPPFH3mLY9pWxsgp",
        "addresses": [
            "T15Egvi9uHA1Jj9hxMJFcuPJ9xo6VTDPPFH3mLY9pWxsgp"
        ]
    }
    

#### Transfering funds

You can submit a transaction from a wallet to an addres by doing a POST with the following data on `/wallets/gen0/transfer`.

    {
        "address": "<the destination address>",
        "amount": "42"
    }

The server must answer succussfully with the transaction id and the group information.

    {
        "txId": "50318e5bfd56796690890f4a9c5aae2725629a15a71cad909bbf4a669c32c2f4",
        "fromGroup": 0,
        "toGroup": 3
    }


#### Query for balance

You can check the current balance of a wallet by doing a GET on `/wallets/foo/balances`.

    {
        "totalBalance": 0,
        "balances": [
            {
                "address": "T1J2yrmQrNwuFW8z2W6xXFLtJoBCWEm7gLg9BuY8tzKjxw",
                "balance": 0
            }
        ]
    }