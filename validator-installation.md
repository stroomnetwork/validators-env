# Validator deployment guide

This is small guide regarding deployment of validator for thirdparty partners.

## Prerequirements

For deployment of validator you'd need the following:

- Linux server with at least 2GiB of memory and reasonable CPU
- Docker installed
- Publicly accessible IP with at least one port open (4444 is advices for unification)

## Step by step

1. Create validator key pair by running `docker run -it public.ecr.aws/g3y5i1b4/key-generator --network testnet generate`
   Note to save key pair securely elsewhere as it could not recovered. Also it’s necessary provide stroom with your
   PUBLIC key to add it to other validators.
2. Create directory `/docker/validator` at server
3. Gather docker-compose.yml and sample.env from stroom
4. Upload docker-compose.yml and sample.env to server where validator will be running and move them to /docker/validator
5. Rename sample.env to .env and update values in it according to your needs
   (for extended setup with own bitcoind and/or ethereum node see references in .env). In basic setup you need to set
   `APPROVAL_THRESHOLD` - provided by stroom
   `BITCOIND_RPCPASSWORD` - provided by stroom
   `BITCOIND_RPCUSER` - provided by stroom
   `ETHEREUM_START_HIGHT` - provided by stroom
   `BITCOIN_START_HIGHT` - provided by stroom
   `VALIDATOR_REGISTRY_CONTRACT` - provided by stroom
   `USER_ACTIVATOR_CONTRACT` - provided by stroom
   `STBTC_CONTRACT` - provided by stroom
   `BSTBTC_CONTRACT` - provided by stroom
   `NODE_PRIVATE_KEY` - your private key from step 1
6. Add other node addresses provided by stroom to docker-compose.yml in corresponding block
7. At specified time run docker compose up -d in directory /docker/validator
